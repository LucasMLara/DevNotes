REDUX


antes de qualquer coisa, vamos iniciar o seu aplicativo react!

se você está clonando um repositório que já possua as dependências no seu packagelock.json, basta um npm (ou o tal do Yarn) install.

se tiver inciando um projeto de 0, você terá que realizar algumas instalações extras:

#1 o npx create-react-app nome-do-seu-app
#2 npm install redux
#3 npm install react- redux
** dica: se vc digitar npm install redux react-redux, vai instalar os 2 de uma vez.
#4 npm install redux-devtools-extension (esse daqui é pra vc não usar aquele link maluco no store para utilizar aquela extensãozinha no seu chrome!)
#5 npm install redux-thunk [CALMA, esse daqui vc não necessariamente precisa instalar, mas já deixo o comando aqui pra facilitar nossa vida depois caso precise!]


agora vai na sua aba lateral do seu leitor de código e crie 3 diretórios:

actions, reducers e store.

e dentro de cada diretório, você irá criar um arquivo js.

geralmente as pessoas colocam o index.js.

DICA: baixe a extensão Material Icon Theme, após baixa-la, clique a engrenagem > extension settings > vai em material-icon-theme: active icon pack e escolha "react_redux"

dessa forma , vc pode criar dentro do diretório store, o arquivo store.js...
repare o íconezinho que vc terá para lhe auxiliar quando seus olhos já não estiverem funcionando tão bem após fritar horas codando.... :D 


viu só??? Massa né??


agora vai la no seu arquivo index.js da pasta src e importe o seu provider!!

mas o que é o provider?

Oras! você está utilizando o Redux juntamente com o React agora. Você precisa PROVER o estado do seu redux para o seu react de alguma forma. 

faça a importação do Provider:

import { Provider } from 'react-redux';

já aproveita e importa o seu store de uma vez:

import store from './store/index'

(ou qualquer local que você tenha definido o seu store. preste atenção nisso!  cada um pode por seu store onde bem entender, basta saber o caminho depois!);

ahh , mas eu não mexi no meu store do redux ainda!!!!

vc já deve ter criado, mas só não escreveu uma bendita linha sequer la dentro! =D

agora vamos resolver isso!

faça sua bateria insana de importações:

import { createStore } from 'redux'; => aqui vc está importando a função que cria a store, vc pode por um applyMiddleware se for necessário, caso vc use aquele "thunk" se comentamos la em cima.

caso vc use applyMiddleWare, faça a importação do thunk

import thunk from 'redux-thunk';

import { composeWithDevTools } from 'redux-devtools-extension'; => aqui nós vamos importar a extensão devTools para utilizar a extensão no seu chrome para fiscalizar as informações dos seus componentes e etc.


e por ultimo , vc vai importar os seus reducers que estarão todos aninhados no arquivo index.js do seu diretório de reducers.

import seuReducerAninhado from 'onde vc tiver colocado o arquivo. verifique com cuidado.'

agora, vamos a função de criação do store:


const store = createStore(
  seuReducerAninhado,
  composeWithDevTools(
    applyMiddleware(thunk),
  ),
);

export default store;

NOSSA!!! Que bagaça é essa? 

é a função createStore que possui como parâmetro, seuReducerAninhado e recebe uma função como parâmetro, que é a composeWithDevTools e que dentro dessa função composeWithDevTools tem OUTRA função que é a applyMiddleware e que possui como parâmetro o thunk.

lets go again!

const store = createStore(seuReducerAninhado,composeWithDevTools(applyMiddleware(thunk)));


export default store;

testa ai, ve se muda alguma coisa! me da um feedback!


lembrando que , se vc não vai usar o thunk, sua importação mudará e sua função de criação da sua store será: 

import { createStore } from 'redux';
import { composeWithDevTools } from 'redux-devtools-extension';
import seuReducerAninhado from 'onde vc tiver colocado o arquivo. verifique com cuidado.';

const store = createStore(
  seuReducerAninhado,
  composeWithDevTools(),
);

export default store;


Agora vamos pensar como será o formato do seu estado global:


 Basicamente, em cada reducer você irá criar seus estados iniciais para trabalhar posteriormente.
 Por exemplo:

const INITIAL_STATE = {
  user: {
    email: '',
  },
};

criamos uma constante para armazenar o estado inicial para melhor legibilidade do código.

 Não entendeu? Fará mais sentido ao ler código abaixo!


const user = (state = INITIAL_STATE, action) => {
  
  switch (action.type) {
  case QUALQUER_COISA:
    return { ...state, action };

  default:
    return { ...state };
  }
};

export default user;


//* nos parâmetros acima, utilizamos o "default parameter" para definir um estado incial, e atribuimos à constante declarate préviamente para não poluir o parâmetro da função com um objeto*//

mas o que é essa action ?

a Action é um objeto que será utilizado como segundo parâmetro do seu reducer (Calma.. já vamos explicar o reducer!)

vamos adiantar a nossa vida e ver como é uma action de uma vez? :D 

eis um exemplo de uma action:

export const user = (payload) => ({
  type: QUALQUER_COISA,
  payload,
});

geralmente , nos arquivos do seu projeto, as actions já são imediatamente exportadas enquanto são criadas, mas você pode fazer suas importações todas agrupadas no final caso seu TOC lhe incomode.

mas o que é esse bendito payload? 
o Payload é onde será armazenado os dados recebidos pela sua "action"*****.
_______________________________



