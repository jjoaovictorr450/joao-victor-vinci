<script setup>
import { computed, ref } from 'vue'

const menuOpen = ref(false)
const mobileOpen = ref(false)
const faqOpen = ref(0)

const vehicles = [
  { name: 'VINCI V1', type: 'CITY', image: 'https://images.unsplash.com/photo-1552519507-da3b142c6e3d?auto=format&fit=crop&w=700&q=85', href: '?modelo=v1' },
  { name: 'VINCI V2', type: 'SUV', image: 'https://images.unsplash.com/photo-1606152421802-db97b9c7a11b?auto=format&fit=crop&w=700&q=85', href: '?modelo=v2' },
  { name: 'VINCI V3', type: 'SPORT', image: 'https://images.unsplash.com/photo-1614200187524-dc4b892 ಹೆಚ್ಚ?auto=format&fit=crop&w=700&q=85', href: '?modelo=v3' },
  { name: 'VINCI V4', type: 'CROSSOVER', image: 'https://images.unsplash.com/photo-1519641471654-76ce0107ad1b?auto=format&fit=crop&w=700&q=85', href: '?modelo=v4' },
  { name: 'VINCI V5', type: 'GRAND TOUR', image: 'https://images.unsplash.com/photo-1549317661-bd32c8ce0db2?auto=format&fit=crop&w=700&q=85', href: '?modelo=v5' },
  { name: 'VINCI V6', type: 'CONCEPT', image: 'https://images.unsplash.com/photo-1503376780353-7e6692767b70?auto=format&fit=crop&w=700&q=85', href: '?modelo=v6' }
]

const selectedKey = new URLSearchParams(window.location.search).get('modelo') || 'v2'
const selected = computed(() => vehicles.find(v => v.href.includes(selectedKey)) || vehicles[1])
const isCarPage = computed(() => window.location.pathname.endsWith('carro.html') || window.location.search.includes('modelo='))
const carTitle = computed(() => `VINCI MODEL ${selectedKey.toUpperCase()}`)
const faqs = [
  { q: 'Qual é a autonomia dos veículos VINCI?', a: 'A autonomia varia de acordo com a versão, bateria, condições de uso e estilo de condução. Consulte as especificações de cada modelo.' },
  { q: 'Quanto tempo leva para carregar a bateria?', a: 'O tempo de recarga depende da capacidade da bateria e da potência do carregador utilizado.' },
  { q: 'Os veículos possuem garantia?', a: 'As condições de garantia são definidas conforme o modelo e os componentes do veículo.' },
  { q: 'Onde posso conhecer os modelos?', a: 'Explore a área de modelos neste site para conhecer a linha VINCI.' }
]
</script>

<template>
  <header class="header">
    <a class="brand" href="./" aria-label="VINCI início">VINCI<span>®</span></a>
    <button class="mobile-toggle" @click="mobileOpen = !mobileOpen" aria-label="Abrir menu">☰</button>
    <nav :class="['nav', { 'nav-open': mobileOpen }]">
      <a href="./">HOME</a>
      <button class="nav-models" @click="menuOpen = !menuOpen" :aria-expanded="menuOpen">MODELOS <span>⌄</span></button>
      <a href="./#experience">EXPERIÊNCIA</a>
      <a href="./#about">SOBRE A VINCI</a>
      <a href="./#contact">CONTATO</a>
    </nav>
    <a class="header-cta" href="./#models">EXPLORE A LINHA <span>↗</span></a>
    <section v-if="menuOpen" class="mega">
      <div class="mega-intro"><small>DESCUBRA A VINCI</small><h3>Uma nova forma<br>de se mover.</h3><a href="./#models">VER TODOS OS MODELOS ↗</a></div>
      <a v-for="v in vehicles" :key="v.name" class="mega-car" :href="`carro.html${v.href}`">
        <img :src="v.image" :alt="v.name"><strong>{{ v.name }}</strong><small>{{ v.type }}</small>
      </a>
    </section>
  </header>

  <main v-if="!isCarPage">
    <section class="home-hero">
      <img class="hero-img" src="https://images.unsplash.com/photo-1593941707882-a5bba14938c7?auto=format&fit=crop&w=2000&q=90" alt="Veículo elétrico conectado a um carregador">
      <div class="hero-shade"></div>
      <div class="hero-copy">
        <p class="eyebrow light">O FUTURO SE MOVE COM VOCÊ</p>
        <h1>Vá além.<br><em>Vá de VINCI.</em></h1>
        <p>Mobilidade elétrica que une design, tecnologia e uma nova maneira de viver a estrada.</p>
        <a class="button button-light" href="#models">DESCUBRA A VINCI <span>↗</span></a>
      </div>
      <div class="hero-index">01 <i></i> 04</div>
    </section>

    <section class="models-section" id="models">
      <div class="section-heading">
        <div><p class="eyebrow">ENGENHARIA EM MOVIMENTO</p><h2>Conheça nossa<br><em>linha elétrica.</em></h2></div>
        <p class="heading-note">Cada modelo foi pensado para transformar sua experiência ao volante. Encontre o VINCI que combina com você.</p>
      </div>
      <div class="featured-grid">
        <a class="featured-car" href="carro.html?modelo=v2">
          <img src="https://images.unsplash.com/photo-1606152421802-db97b9c7a11b?auto=format&fit=crop&w=1200&q=85" alt="VINCI Model V2">
          <div><small>01 / SUV ELÉTRICO</small><h3>VINCI MODEL V2</h3><span>CONHEÇA O MODELO ↗</span></div>
        </a>
        <a class="featured-car" href="carro.html?modelo=v3">
          <img src="https://images.unsplash.com/photo-1503376780353-7e6692767b70?auto=format&fit=crop&w=1200&q=85" alt="VINCI Model V3">
          <div><small>02 / PERFORMANCE</small><h3>VINCI MODEL V3</h3><span>CONHEÇA O MODELO ↗</span></div>
        </a>
      </div>
    </section>

    <section class="campaign" id="experience">
      <img src="https://images.unsplash.com/photo-1551830820-330a71b99659?auto=format&fit=crop&w=2000&q=85" alt="Carro elétrico em ambiente moderno">
      <div class="campaign-copy"><p class="eyebrow light">O AMANHÃ COMEÇA AGORA</p><h2>Silêncio por fora.<br><em>Revolução por dentro.</em></h2><a class="button button-light" href="carro.html?modelo=v2">SINTA A EXPERIÊNCIA ↗</a></div>
    </section>

    <section class="all-models" id="about">
      <div class="section-heading compact"><div><p class="eyebrow">A FAMÍLIA VINCI</p><h2>Design que inspira.<br><em>Tecnologia que move.</em></h2></div><a class="text-link" href="#" @click.prevent="menuOpen = true">EXPLORAR MODELOS ↗</a></div>
      <div class="vehicle-strip">
        <a v-for="v in vehicles.slice(0,3)" :key="v.name" :href="`carro.html${v.href}`"><img :src="v.image" :alt="v.name"><span>{{ v.name }} <b>↗</b></span></a>
      </div>
    </section>
  </main>

  <main v-else>
    <section class="car-intro">
      <div class="car-intro-copy"><p class="eyebrow">A NOVA GERAÇÃO ELÉTRICA</p><h1>{{ carTitle }}</h1><p>Uma combinação extraordinária de design, tecnologia e performance. Descubra uma nova experiência de condução.</p><div class="car-actions"><a class="button button-dark" href="#specs">CONHEÇA O MODELO ↗</a><a class="under-link" href="./#models">VER OUTROS MODELOS</a></div></div>
      <img class="car-main-image" :src="selected.image" :alt="selected.name">
      <div class="quick-stats"><div><strong>520<span> km</span></strong><small>AUTONOMIA*</small></div><div><strong>3,8<span> s</span></strong><small>0–100 KM/H*</small></div><div><strong>100<span>%</span></strong><small>ELÉTRICO</small></div></div>
    </section>
    <section class="panorama"><img src="https://images.unsplash.com/photo-1503376780353-7e6692767b70?auto=format&fit=crop&w=2000&q=90" alt="Detalhe do veículo VINCI"><div class="panorama-label">DESIGN QUE DESAFIA O CONVENCIONAL</div></section>
    <section class="spec-section" id="specs"><p class="eyebrow">PENSADO EM CADA DETALHE</p><h2>Mais do que dirigir.<br><em>É sentir a diferença.</em></h2><div class="spec-grid"><article><b>01</b><h3>Design marcante</h3><p>Linhas aerodinâmicas e proporções que traduzem personalidade.</p></article><article><b>02</b><h3>Tecnologia intuitiva</h3><p>Uma experiência conectada, simples e inteligente.</p></article><article><b>03</b><h3>Performance elétrica</h3><p>Resposta imediata e condução suave em cada trajeto.</p></article><article><b>04</b><h3>Conforto absoluto</h3><p>Um espaço criado para acompanhar seu ritmo.</p></article></div></section>
    <section class="gallery"><img src="https://images.unsplash.com/photo-1492144534655-ae79c964c9d7?auto=format&fit=crop&w=900&q=85" alt="Detalhe automotivo"><img src="https://images.unsplash.com/photo-1503376780353-7e6692767b70?auto=format&fit=crop&w=900&q=85" alt="Design do veículo"><img src="https://images.unsplash.com/photo-1549317661-bd32c8ce0db2?auto=format&fit=crop&w=900&q=85" alt="Veículo em movimento"><img src="https://images.unsplash.com/photo-1606152421802-db97b9c7a11b?auto=format&fit=crop&w=900&q=85" alt="Interior e exterior"></section>
    <section class="faq-section"><p class="eyebrow">AINDA TEM DÚVIDAS?</p><h2>Perguntas frequentes</h2><div class="faq-list"><article v-for="(f,i) in faqs" :key="f.q" :class="{ active: faqOpen === i }"><button @click="faqOpen = faqOpen === i ? -1 : i">{{ f.q }} <span>{{ faqOpen === i ? '−' : '+' }}</span></button><p v-if="faqOpen === i">{{ f.a }}</p></article></div></section>
  </main>

  <footer class="footer" id="contact"><div class="footer-top"><a class="brand brand-footer" href="./">VINCI<span>®</span></a><p>O futuro da mobilidade<br>começa com uma escolha.</p><a class="back-top" href="#">VOLTAR AO TOPO ↑</a></div><div class="footer-bottom"><span>© 2026 VINCI ELECTRIC VEHICLES</span><span>PROJETO ACADÊMICO • DESIGN CONCEITUAL</span></div></footer>
</template>