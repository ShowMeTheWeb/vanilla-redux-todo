# Vanilla Redux Todo

Learning Vanilla-Redux
* * *
### Setup
1. npx create-react-app vanilla-redux-todo
2. yarn add redux
* * *
### 
- Store : data를 저장하는 곳
```js
const store = createStore(reducer);
```
- createStore : reducer를 요구함 (reducer 함수 정의)
```js
const reducer = (state = [], action) => {
  switch (action.type) {
    case ADD_TODO:
      const newTodoObj = { text: action.text, id: Date.now() };
      return [newTodoObj, ...state];
    case DELETE_TODO:
      const cleaned = state.filter(toDo => toDo.id !== action.id);
      return cleaned;
    default:
      return state;
  }
};
```
- subscribe : store안에 변화에 대해 알 수 있음.
```js
store.subscribe(() => console.log(store.getState()));

store.subscribe(paintToDos);
```
- dispatch : reducer 함수로 action을 보내는 방법
```js
const dispatchAddToDo = (text) => {
  store.dispatch(addToDo(text));
};

const dispatchDeleteTodo = (e) => {
  const id = parseInt(e.target.parentNode.id);
  store.dispatch(delteTodo(id));
};
```
- paintToDos : 화면에 TODO를 보이게함. 다 지우고 다시 그리는 단점이있음.
```js
const paintToDos = () => {
  const toDos = store.getState();
  ul.innerHTML = "";
  toDos.forEach((toDo) => {
    const li = document.createElement("li");
    const btn = document.createElement("button");
    btn.innerText = "DEL";
    btn.addEventListener("click", dispatchDeleteTodo);
    li.id = toDo.id;
    li.innerText = toDo.text;
    li.appendChild(btn);
    ul.appendChild(li);
  });
};
```