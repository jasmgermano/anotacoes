# React

area: front-end

## Introdução

### O que é react?

- react é uma biblioteca javascript (não um framework) para construção de interfaces
- responsável apenas por construir interfaces de usuário
- nos permite criar grandes aplicativos da web que podem alterar os dados sem recarregar a página da web
- react possui uma arquitetura baseada em componentes, isso permite que vc divida sua aplicação em partes encapsuladas que podem ser compostas para criar UI’s mais complexas
- componentes podem ser reutilizados em outras linguagens
- reagir é declarativo - diga a reação o que você deseja e a reação criará a interface do usuário real

## Primeiro projeto

```jsx
npm create-react-app meu-projeto
```

*Isso é de uma documentação antiga. **Go to [react.dev](https://react.dev/) for the new React docs.**

## JXS

- tipo HTML, mas dentro do código javascript
- É a principal maneira de escrever HTML com o react
- é possível interpolar variáveis (inserindo ela entre {}), executar funções em jsx e inserir valores em atributos de tags

## Componentes

- permite dividir a aplicação em partes

### Criando componentes

meu-projeto > src > ***components > helloworld.js*** 

```jsx
function HelloWorld() {
	return (
		<div>
			<h1> Meu primeiro componente </h1>
		</div>
	)
}

export default HelloWord
```

- É necessário importar o componente e chama-lo

meu-projeto > src  ***> app.js*** 

```jsx
// importando
import './App.css'
import HelloWorld from './components/HelloWorld'

function App() {
	...
	return (
		...
		<HelloWorld />
	)
}
...
```

- Os componentes devem ser reutilizaveis
    - não necessariamente ele tem que ser exportado para o app.js, podendo ser usado no helloword anterior, por exemplo

meu-projeto > src > ***components > frase.js*** 

```jsx
function Frase() {
	return (
		<div>
			<p> Este é um componente com uma frase </p>
		</div>
	)
}

export default Frase
```

meu-projeto > src > ***components > helloworld.js*** 

```jsx
import Frase from './components/Frase'

function HelloWorld() {
	return (
		<div>
			<Frase />
			<h1> Meu primeiro componente </h1>
			<Frase />
			<Frase />
			<Frase />
		</div>
	)
}

export default HelloWord
```

---

Este é um componente com uma frase!

# Meu primeiro componente

Este é um componente com uma frase!

Este é um componente com uma frase!

---

## Props

- São os valores passados para os componentes, para fazer com que os componentes ficam dinâmicos, ou seja, mudar a execução por causa do valor do prop
- O valor é passado como um atributo na chamada do componente e precisa ser resgatado dentro de uma propriedade/argumento
- são somente leitura

meu-projeto > src  ***> components > SayMyName.js*** 

```jsx
function SayMyName(props) {
	return (
		<div>
			<p>Fala aí {props.nome}, suave?</p>
		</div>
	)
}

export default SayMyName
```

meu-projeto > src  ***> app.js*** 

```jsx
// importando
import './App.css'
import HelloWorld from './components/HelloWorld'
import SayMyName from './components/SayMyName'

function App() {
	...
	return (
		...
		<HelloWorld />
		<SayMyName nome="Matheus" />
	)
}
...
```

---

Fala aí Matheus, suave?

---

```jsx
// importando
import './App.css'
import HelloWorld from './components/HelloWorld'
import SayMyName from './components/SayMyName'

function App() {
	const nome = 'Maria'
	...
	return (
		...
		<HelloWorld />
		<SayMyName nome="Matheus" />
		<SayMyName nome={nome} />
	)
}
...
```

---

Fala aí Matheus, suave?

Fala aí Maria, suave?

---

meu-projeto > src  ***> components > Pessoa.js*** 

```jsx
// é possivel desestruturar o props
function Pessoa({nome, idade, profissao, foto}) {
	return (
		<div>
			<img src={foto} alt={nome} />
      <h2>Nome: {nome}</h2>
      <p>Idade: {idade}</p>
      <p>Profissão: {profissao}</p>
		</div>
	)
}

export default Pessoa
```

meu-projeto > src  ***> app.js*** 

```jsx
// importando
import './App.css'
import HelloWorld from './components/HelloWorld'
import SayMyName from './components/SayMyName'

function App() {
	...
	return (
		...
		<HelloWorld />
		<SayMyName nome="Matheus" />
		<Pessoa 
			nome="Jasmine"
			idade="22"
			profisao="programadora"
			foto="#link" />
	)
}
...
```