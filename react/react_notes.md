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
import Pessoa from './components/Pessoa'

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

## Adicionando CSS

- Pode ser adicionado de forma global, por meio do arquivo `index.css`, por exemplo
- Também é possível estilizar a nível de componentes
    - CSS modules
        1. Criar `Componente.module.css`
        2. Chamar no componente

meu-projeto > src  ***> components > frase.module.css***

```css
.fraseContainer {
	background-color: #333;
	border: 1px solid #111;
}

.fraseContent {
	color: #fff;
	background-color: #333;
	margin: 0;
}
```

meu-projeto > src > ***components > frase.js***

```jsx
import styles from '/frase.module.css'

function Frase() {
	return (
		<div className={styles.fraseContainer}>
			<p>Este é um componente com uma frase!</p>
		</div>
	)
}

export default Frase
```

meu-projeto > src > ***app.js***

```jsx
// importando
import './App.css'
import HelloWorld from './components/HelloWorld'
import SayMyName from './components/SayMyName'
import Pessoa from './components/Pessoa'
import Frase from './components/Frase'

function App() {
	...
	return (
		...
		<HelloWorld />
		<Frase />
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

## Fragmentos

- Permite a criação de componentes sem elemento pai
- Descomplicar os nós do dom
- A sintaxe é `<>` e `</>` , não é necessário um nome para a tag

meu-projeto > src > ***components > List.js***

```jsx
function List() {
	return (
		<div>
			<h1>Minha lista</h1>
			<ul>
				<li> Item 1 </li>
				<li> Item 2 </li>
			</ul>
		</div>
	)
}

export default List
```

- A div não faz sentido, pode ser desnecessária e poluir o código. Por isso usamos o react fragments.

meu-projeto > src > ***components > List.js***

```jsx
function List() {
	return (
		<>
			<h1>Minha lista</h1>
			<ul>
				<li> Item 1 </li>
				<li> Item 2 </li>
			</ul>
		</>
	)
}

export default List
```

```markdown
# Nem sempre a div é desnecessária, pode ser útil para criar um card, por exemplo. Quando não é o caso, o react fragments é usado pra simplicar o DOM, já que é um elemento a menos sendo criado. 
```

## Avançando em props

- Definir tipos para as props
    - Definindo em um objeto `propTypes` no próprio componente
- Definir um valor padrão
    - Utilizando o objeto `defaultProps`

meu-projeto > src > ***components > List.js***

```jsx
import Item from './Item'
function List() {
	return (
		<>
			<h1>Minha lista</h1>
			<ul>
				<Item marca="Ferrari" ano_lancamento={1985} />
				<Item marca="Fiat" ano_lancamento={1964} />
				<Item marca="Renault" />
			</ul>
		</>
	)
}

export default List
```

meu-projeto > src > ***components > Item.js***

```jsx
import PropTypes from 'prop-types' // ja vem com o react

function Item({ marca, ano_lancamento }) {
	return (
		<>
			<li> 
				{marca} - {ano_lancamento}
			</li>
		</>
	)
}

Item.propTypes = { // perceba que o propTypes é com letra minuscula
	marca: PropTypes.string.isRequired,
	ano_lancamento: PropTypes.numer,
}

Item.defaultProps = {
	marca: 'Faltou a marca',
	ano_lancamento: 0,
}

export default Item
```

- Se colocarmos `marca={1}` vai aparecer um erro no console.
- Se deixarmos em branco também, pois colocamos o `isRequired`