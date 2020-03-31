### hooks todolist with localstorage

![todo](https://user-images.githubusercontent.com/26340566/78045560-b06f3700-73a8-11ea-9677-fd8a13ddfe4f.png)

> 副作用的顺序会影响程序的正确执行

- 如果下面这样，默认 `todo` 是空数组，所以 `localstorage` 的值不会拿到，一直是空的。
- set 空数组也会触发副作用

```
useEffect(() => {
      localStorage.setItem('todos', JSON.stringify(todos))
  }, [todos])

useEffect(() => {
      console.log("localStorage.getItem('todos')", localStorage.getItem('todos'))
      const todos = JSON.parse(localStorage.getItem('todos')) || []
      setTodos(todos)
  }, [])
```

你需要交换顺序
```
useEffect(() => {
  console.log("localStorage.getItem('todos')", localStorage.getItem('todos'))
  const todos = JSON.parse(localStorage.getItem('todos')) || []
  setTodos(todos)
}, [])

useEffect(() => {
  localStorage.setItem('todos', JSON.stringify(todos))
}, [todos])
    
```
