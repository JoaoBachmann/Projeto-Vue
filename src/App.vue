<script setup>
import { ref, reactive, computed } from "vue";  
const booleano = ref(true);
</script>

<template>
  <header>
    <div class="titulo">
      <p class="um">
        IFbooks
      </p>
      <p class="dois">
        a preço a<br>leitura
      </p>
    </div>
    <div class="barra-pesquisa">
      <input type="text" placeholder="Código do Cupom" name="search">
      <button type="submit" class="fas fa-search icone-pesquisa"></button>
    </div>
    <div>
      <ul class="page">
        <li>
          Termos
        </li>
        <li>
          Equipe
        </li>
        <li>
          Envio
        </li>
        <li>
          Devoluções
        </li>
      </ul>
    </div>
    <div>
      <ul class="icon">
        <li>
          <i class="fa-solid fa-cart-shopping" @click="booleano = !booleano"></i>
        </li>
        <li class="icone">
          <i class="fa-solid fa-heart"></i>
        </li>
        <li>
          <i class="fa-solid fa-user"></i>
        </li>
        <li></li>
      </ul>
    </div>
  </header>

  <body>


    <section class="autorL" v-if="booleano">
      <div class="sobreA">
        <p class="autor">Autor de Abril</p>
        <h2 class="negrito">Eric-Emanuel Schmitt</h2>
        <p class="texto">
          Eric-Emmanuel Schmitt has been awarded more than 20 literary prizes and distinctions, and
          in 2001 he received the title of Chevalier des Arts et des Lettres. His books have been
          translated into over 40 languages.
        </p>
        <button>
          <a href="#"></a>
          Acessar página do livro</button>
      </div>

      <div class="fotoLivro">
        <img src="/public/Imagens/book.png" alt="livro" />
        <p>*within the stock limit</p>
      </div>
    </section>

    <section class="opcoes" v-if="booleano">
      <div class="linha">
        <i class="fa-solid fa-truck"></i>
        <p>Frete grátis para SC</p>
      </div>
      <div class="linha">
        <i class="fa-solid fa-star"></i>
        <p>Livros recomendados</p>
      </div>
      <div>
        <i class="fa-solid fa-book-open"></i>
        <p>Mais vendidos</p>
      </div>
    </section>

    <section class="listalivros" v-if="booleano">
      <h1>Lista de Livros</h1>
      <div v-for="produto in produtos" :key="produto.id" class="livro">
        <img :src="produto.capa" alt="" width="100%" height="100%" />
        <h2>{{ produto.titulo }}</h2>
        <p class="res">{{ produto.resenha }}</p>
        <strong>R$ {{ produto.preco.toFixed(2).replace(".", ",") }}</strong>
        <br>
        <button class="compra" @click="adicionar(produto), booleano = !booleano">
          <i class="fa-solid fa-cart-shopping"></i>
          <p>comprar</p>
        </button>

      </div>
    </section>
    <section class="carrinho" v-else>
      <h1>Carrinho</h1>
      <div class="titulos">
        <h2>
          Titulos
        </h2>
        <h2 class="qnt">
          Quantidade
        </h2>
        <h2>
          subtotal
        </h2>
      </div>
      <div v-for="item in carrinho.items" :key="item.id" class="  itensCarrinhos">
        <div class="maior">
          <img class="imgCarrinho" :src="item.capa" alt="">
          <div>
            <h2>{{ item.titulo }}</h2>
            <p>{{ item.resenha }}</p>
            <strong>R${{ item.preco.toFixed(2).replace(".", ",") }}</strong>
          </div>
        </div>
        <div class="contador">
          <button @click="decrementar(item)">-</button>
          <input type="number" min="1" v-model.number="item.quantidade" @change="arredondar(item)">
          <button @click="incrementar(item)">+</button>
        </div>
        <strong class="preco">R${{ (item.preco * item.quantidade).toFixed(2).replace(".", ",") }}</strong>
      </div>
      <button class="butao" @click="booleano = true">Voltar para loja</button>
      <ul class="principal">
        <li class="cupom">
          <input type="text" placeholder="Código do Cupom" name="search">
          <button type="submit">Inserir Cupom</button>
        </li>
        <li class="totalC">
          <h2>Total da Compra</h2>
          <div class="maiorFinal">
            <div>
              <p>Produtos:</p>
              <strong>{{ carrinho.items.length }}</strong>
            </div>
            <div class="border">
              <p>Frete:</p>
              <strong>Gratis</strong>
            </div>
            <div>
              <p>Total:</p>
              <strong>R$ {{ totalCarrinho() }}</strong>
            </div>
          </div>
          <button>Ir Para o Pagamento</button>
        </li>
      </ul>
    </section>
  </body>
  <footer>
    <div class="pe">
      <div class="unha">
        <p>IFbooks</p>
        <i class="fa-brands fa-square-facebook"></i>
        <i class="fa-brands fa-square-instagram"></i>
        <i class="fa-brands fa-square-x-twitter"></i>
      </div>
      <div class="ifbook">
        <p>Contato</p>
        <div class="redes">
          <i class="fa-solid fa-phone"> </i>
          <p>+55 47 40045263</p>
        </div>
        <div class="redes">
          <i class="fa-solid fa-clock"> </i>
          <p>8h às 23h - Seg a Sex</p>
        </div>
        <div class="redes">
          <i class="fa-solid fa-envelope"></i>
          <p>contato@ifbooks.com</p>
        </div>
        <div class="img">
          <img src="../public/Imagens/paipal 1.png" alt="paypal">
          <img src="../public/Imagens/MasterCard-Logo-1979 1.png" alt="Master Card">
          <img src="../public/Imagens/VISA-card-logo- 1.png" alt="Visa">
        </div>
      </div>
    </div>
    <div class="theLast">
      <P>© Alguns direitos reservados. IFbooks 2025. </P>
    </div>
  </footer>

</template>

<style scoped>

</style>
