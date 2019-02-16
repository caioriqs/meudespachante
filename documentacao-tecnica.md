> Especialista Digital Analytics: Caio Gomes<br />
> Documento de Especificação Técnica - Meu Despachante

<br />

## Implementação da Camada de dados
Última atualização: 02/02/2019<br />
Em caso de dúvidas, entrar em contato com: [silva.caiohenrique@gmail.com](mailto:silva.caiohenrique@gmail.com)

<br />

## Índice
- [Objetivo](#objetivo)
- [Overview e Descrições Técnicas](#overview-e-descrições-técnicas)
- [Dimensões Globais](#dimensões-globais)
- [Especificação de Micro-conversões](#especificação-de-micro-conversões)
- [Especificação de Conversões](#especificação-de-conversões)
- [Considerações Finais](#considerações-finais)

<br />

## Objetivo
Este documento tem como objetivo instruir a implementação do Google Tag Manager, da camada de dados e de data attributes para utilização de recursos de monitoramento do Google Analytics referentes ao ambiente de [Meu Despachante](https://www.meudespachante.com.br/).

<br />

## Overview e Descrições Técnicas



### Camada de dados (DataLayer)

> É um array de objetos javascript utilizado pelo Google Tag Manager para receber em seus atributos, dados importantes do site.
Para implementar o dataLayer no site, o desenvolvedor pode utilizar formas diferentes para preencher os dados. Essas formas são dependentes da ação estabelecida na documentação e também do nível da interação.

**Instalação**<br />
Inserir a camada de dados antes do snippet de instalação do Google Tag Manager. Exemplo:

```html
<script>
	window.dataLayer = window.dataLayer || [];
	window.dataLayer = [{
		'atributo1': '[[valor1]]',
		'atributo2': '[[valor2]]'
	}];
</script>
```

OU

```html
<script>
	window.dataLayer = window.dataLayer || [];
	window.dataLayer.push({
		'atributo1': '[[valor1]]',
		'atributo2': '[[valor2]]'
	});
</script>
```

### Atributos HTML (Data Attributes)

> São atributos customizados inseridos nos elementos HTML da página que permite a inclusão de dados adicionais.

**Instalação**
1. Elementos de link: ```<a href="..." class="minha_classe">Link</a>``` <br />
Elementos do tipo link que foram mapeados, precisam receber a classe **gtm-link-event** e os data attributes em sua estrutura.

```html
<a href="http://www.meudominio.com.br/page2"
	class="minha_classe gtm-link-event"
 	gtm-event-data-category="[[exemplo:valor-categoria]]"
  	gtm-event-data-action="[[exemplo:valor-acao]]"
  	gtm-event-data-label="[[exemplo:valor-rotulo]]">Texto do link</a>
```

2. Elementos comuns: ```<div class="minha_classe">Elemento</div>``` <br />
Todos os elementos comuns do html que não são links e que foram mapeados, precisam receber a classe **gtm-element-event** em sua estrutura.

```html
<div 	class="minha_classe gtm-element-event"
  	gtm-event-data-category="[[exemplo:valor-categoria]]"
 	gtm-event-data-action="[[exemplo:valor-acao]]"
 	gtm-event-data-label="[[exemplo:valor-rotulo]]">Texto do elemento</div>
```

#### Importante:
> Todos os links e botões citados nesta documentação devem ter em sua estrutura `html` a classe `gtm-link-event` se for um link `<a>` ou `gtm-element-event` se o elemento não for um link `<a>` conforme demonstraremos nos exemplos específicos.<br />

> Devem ter também os data-attributes `gtm-event-data-category`, `gtm-event-data-action` e `gtm-event-data-label` preenchidos conforme instruções específicas.

<br />	 	

## Implementação

A documentação foi descrita para algumas áreas especificas do ambiente [Meu Despachante](https://www.meudespachante.com.br/).


### Especificações Globais:

**Itens Gerais:**<br />
Todas as informações entre colchetes `[[  ]]` são variáveis dinâmicas que devem ser preenchidas com seus respectivos valores; <br />
Todos os valores enviados ao Google Analytics devem estar sanitizados, ou seja, sem espaços, acentuação ou caracteres especiais; <br />
Caso a informação solicitada não estiver disponível retornar 'nao_disponivel'. - Mudar de acordo com o projeto

---

<br />

### Especificação de Micro-conversões:


**1 - Clique no Menu:**<br />

- **Quando:** Ao clicar em qualquer item do menu;
- **Onde:** Menu principal;

```html
<!-- Use se o elemento for um link -->
<a href="#"
	class="gtm-link-event"
	gtm-event-data-category="meu-despachante:home"
	gtm-event-data-action="clique:menu"
	gtm-event-data-label="menu:[[nome-item]]"
>Link</a>

<!-- Use se o elemento não for um link -->
<i 	class="gtm-element-event"
	gtm-event-data-category="meu-despachante:home"
	gtm-event-data-action="clique:menu"
	gtm-event-data-label="menu:[[nome-item]]"
>Botão</i>
```

| Variável 			| Exemplo 											| Descrição				|
| :----------------	| :------------------------------------------------	| :-------------------	|
| [[nome-item]]		| 'sobre-nos', 'blog', 'tabela-vencimentos'	e etc	| Nome do item no Menu	|

<br />

**2 - Acessar Minha Conta:**<br />

- **Quando:** Ao clicar em "Minha Conta";
- **Onde:** Menu principal;

```html
<!-- Use se o elemento for um link -->
<a href="#"
	class="gtm-link-event"
	gtm-event-data-category="meu-despachante:home"
	gtm-event-data-action="clique:menu"
	gtm-event-data-label="minha-conta:acessar"
>Link</a>

<!-- Use se o elemento não for um link -->
<i 	class="gtm-element-event"
	gtm-event-data-category="meu-despachante:home"
	gtm-event-data-action="clique:menu"
	gtm-event-data-label="minha-conta:acessar"
>Botão</i>
```


<br />

**3 - Link "Consultar regulamento":**<br />

- **Quando:** Ao clicar no link do regulamento;
- **Onde:** Content principal "Ganhe Licenciamento" - acima do campo de busca;

```html
<!-- Use se o elemento for um link -->
<a href="#"
	class="gtm-link-event"
	gtm-event-data-category="meu-despachante:home"
	gtm-event-data-action="clique:link"
	gtm-event-data-label="ganhe-licenciamento:consulte-regulamento"
>Link</a>

<!-- Use se o elemento não for um link -->
<i 	class="gtm-element-event"
	gtm-event-data-category="meu-despachante:home"
	gtm-event-data-action="clique:link"
	gtm-event-data-label="ganhe-licenciamento:consulte-regulamento"
>Botão</i>
```

<br />


**4 - Clique Buscar:**<br />

- **Quando:** Ao clicar no botão "Buscar";
- **Onde:** Content Principal - consulte débitos do veículo;

```html
<!-- Use se o elemento for um link -->
<a href="#"
	class="gtm-link-event"
	gtm-event-data-category="meu-despachante:buscar"
	gtm-event-data-action="clique:buscar"
	gtm-event-data-label="consulte-debitos"
>Link</a>

<!-- Use se o elemento não for um link -->
<i 	class="gtm-element-event"
	gtm-event-data-category="meu-despachante:buscar"
	gtm-event-data-action="clique:buscar"
	gtm-event-data-label="consulte-debitos"
>Botão</i>
```

<br />

**5 - Clique "Perguntas":**<br />

- **Quando:** Ao clicar em "ver mais perguntas" ;
- **Onde:** Sessão de dúvidas frequentes;

```html
<!-- Use se o elemento for um link -->
<a href="#"
	class="gtm-link-event"
	gtm-event-data-category="meu-despachante:home"
	gtm-event-data-action="clique:duvidas-frequentes"
	gtm-event-data-label="ver-mais-perguntas"
>Link</a>

<!-- Use se o elemento não for um link -->
<i 	class="gtm-element-event"
	gtm-event-data-category="meu-despachante:home"
	gtm-event-data-action="clique:duvidas-frequentes"
	gtm-event-data-label="ver-mais-perguntas"
>Botão</i>
```

<br />

**6 - Clique "+ Perguntas":**<br />

- **Quando:** Ao clicar nas dúvidas;
- **Onde:** Sessão de dúvidas frequentes;

```html
<!-- Use se o elemento for um link -->
<a href="#"
	class="gtm-link-event"
	gtm-event-data-category="meu-despachante:home"
	gtm-event-data-action="clique:duvidas-frequentes"
	gtm-event-data-label="[[nome-duvida]]"
>Link</a>

<!-- Use se o elemento não for um link -->
<i 	class="gtm-element-event"
	gtm-event-data-category="meu-despachante:home"
	gtm-event-data-action="clique:duvidas-frequentes"
	gtm-event-data-label="[[nome-duvida]]"
>Botão</i>
```

| Variável 		| Exemplo 								| Descrição								|
| :-----------	| :----------------------------------	| :----------------------------------	|
| nome-duvida	| 'porque-utilizar-o-meu-despachante' 	| Nome da dúvida clicada, sanitizada	|

<br />


**7 - Clique Rodapé:**<br />

- **Quando:** Ao clicar em algum item/link;
- **Onde:** Rodapé;

```html
<!-- Use se o elemento for um link -->
<a href="#"
	class="gtm-link-event"
	gtm-event-data-category="meu-despachante:home"
	gtm-event-data-action="clique:rodape"
	gtm-event-data-label="link:[[nome-link]]"
>Link</a>

<!-- Use se o elemento não for um link -->
<i 	class="gtm-element-event"
	gtm-event-data-category="meu-despachante:home"
	gtm-event-data-action="clique:rodape"
	gtm-event-data-label="link:[[nome-link]]"
>Botão</i>
```

| Variável 		| Exemplo 								| Descrição							|
| :-----------	| :----------------------------------	| :-------------------------------	|
| nome-link		| 'licenciamento-2019', 'fale-conosco' 	| Nome do link clicado, sanitizado	|

<br />


**8 - Consultar outro veículo:**<br />

- **Quando:** Ao clicar no botão de "Consultar outro veículo";
- **Onde:** No box de sucesso de consulta;

```html
<!-- Use se o elemento for um link -->
<a href="#"
	class="gtm-link-event"
	gtm-event-data-category="meu-despachante:consultar"
	gtm-event-data-action="clique:consultar-outro-veiculo"
	gtm-event-data-label="box-sucesso"
>Link</a>

<!-- Use se o elemento não for um link -->
<i 	class="gtm-element-event"
	gtm-event-data-category="meu-despachante:consultar"
	gtm-event-data-action="clique:consultar-outro-veiculo"
	gtm-event-data-label="box-sucesso"
>Botão</i>
```

<br />

**9 - Blog - Clique Menu:**<br />

- **Quando:** Ao clicar nos itens
- **Onde:** Menu Blog

```html
<!-- Use se o elemento for um link -->
<a href="#"
	class="gtm-link-event"
	gtm-event-data-category="meu-despachante:blog"
	gtm-event-data-action="clique:menu"
	gtm-event-data-label="menu:[[nome-item]]"
>Link</a>

<!-- Use se o elemento não for um link -->
<i 	class="gtm-element-event"
	gtm-event-data-category="meu-despachante:blog"
	gtm-event-data-action="clique:menu"
	gtm-event-data-label="menu:[[nome-item]]"
>Botão</i>
```

| Variável 			| Exemplo 					| Descrição				|
| :----------------	| :---------------------	| :-------------------	|
| [[nome-item]]		| 'cnh', 'multas' e etc		| Nome do item no Menu	|

<br />

---

### Especificação de Conversões:

**Sucesso Consulta:**<br />

- **Onde:** No callback de sucesso .

```html
<script>
	dataLayer.push({
		'event': 'conversion',
		'eventCategory': 'meu-despachante:consultar',
		'eventAction': 'sucesso:consulta
'	});
</script>
```

<br />

## Considerações Finais:

> Link de referência: [Documentação Oficial Google Tag Manager](https://developers.google.com/tag-manager/quickstart)
