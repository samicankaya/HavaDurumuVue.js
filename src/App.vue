<script setup>
import { ref, onMounted } from 'vue'


const arananSehir = ref('Kahramanmaraş') 
const havaVerisi = ref(null) 
const yukleniyor = ref(false)
const hata = ref(false)

const havayiGetir = async () => {
  if (arananSehir.value.trim() === '') return
  
  yukleniyor.value = true
  hata.value = false
  havaVerisi.value = null

  try {
    const yanit = await fetch(`https://wttr.in/${arananSehir.value}?format=j1`)
    
    if (!yanit.ok) throw new Error('Şehir bulunamadi')
    
    const veri = await yanit.json()
    
    havaVerisi.value = {
      isim: arananSehir.value, 
      sicaklik: veri.current_condition[0].temp_C,
      hissedilen: veri.current_condition[0].FeelsLikeC,
      nem: veri.current_condition[0].humidity,
      durum: veri.current_condition[0].weatherDesc[0].value
    }
    
    arananSehir.value = '' 
  } catch (err) {
    hata.value = true
  } finally {
    yukleniyor.value = false
  }
}

onMounted(() => {
  havayiGetir()
})
</script>

<template>
  <div class="hava-kutu">
    <h1>Hava Durumu</h1>
    
    <form @submit.prevent="havayiGetir" class="arama-alani">
      <input v-model="arananSehir" placeholder="Bir şehir veya ilçe yazın..." />
      <button type="submit">Ara</button>
    </form>

    <div v-if="yukleniyor" class="mesaj">Veriler getiriliyor...</div>
    <div v-else-if="hata" class="mesaj hata">Şehir bulunamadı veya bağlantı hatası.</div>

    <div v-else-if="havaVerisi" class="hava-karti">
      <h2 class="sehir-ismi">{{ havaVerisi.isim.toUpperCase() }}</h2>
      <div class="sicaklik">{{ havaVerisi.sicaklik }}°C</div>
      <div class="detaylar">
        <p><strong>Hissedilen:</strong> {{ havaVerisi.hissedilen }}°C</p>
        <p><strong>Nem Orani:</strong> %{{ havaVerisi.nem }}</p>
        <p><strong>Durum:</strong> {{ havaVerisi.durum }}</p>
      </div>
    </div>
  </div>
</template>

<style>
.hava-kutu {
  max-width: 400px;
  margin: 50px auto;
  font-family: sans-serif;
  text-align: center;
}
.arama-alani {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
}
.arama-alani input {
  flex: 1;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
}
.arama-alani button {
  padding: 10px 20px;
  background-color: #0984e3;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}
.mesaj {
  padding: 20px;
  font-size: 1.1em;
  color: #636e72;
}
.hata {
  color: #d63031;
}
.hava-karti {
  background: linear-gradient(135deg, #74b9ff, #0984e3);
  color: white;
  padding: 30px;
  border-radius: 10px;
  box-shadow: 0 4px 15px rgba(0,0,0,0.1);
}
.sehir-ismi {
  margin-top: 0;
  font-size: 1.5em;
  border-bottom: 1px solid rgba(255,255,255,0.3);
  padding-bottom: 10px;
}
.sicaklik {
  font-size: 4em;
  font-weight: bold;
  margin: 10px 0;
}
.detaylar {
  background: rgba(0,0,0,0.1);
  padding: 15px;
  border-radius: 8px;
  text-align: left;
}
.detaylar p {
  margin: 5px 0;
}
</style>