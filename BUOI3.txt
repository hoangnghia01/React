import logo from './logo.svg';
import './App.css';
import Studentlist from './Studentlist'
import { useState } from "react"

function App() {

  const [x, setX] = useState(0);
  const [text, setText] = useState('Meo');
  const [name, setName] = useState('')
  const [check, setCheck] = useState(true)

  const [list, setList] = useState([1, 2, 3, 4]);
  const dsvd = [{ name: 'Heo', old: 2 }, { name: 'Ga', old: 3 }]

  const [list_dv, setList_dv] = useState(() => {
    let listLocal;
    if (localStorage.getItem("list_sinhvien")) {
      listLocal = JSON.parse(localStorage.getItem("list_sinhvien"))
    }
    else {
      listLocal = dsvd;
    }
    return listLocal;
  });


  const handle_increase = () => {
    setX((pre) => pre + 1);
    setX((pre) => pre + 1);
  }
  const [student, setStudent] = useState({
    name: "Hoang Nghia",
    old: 12,
  });

  const handle_Changetext = (e) => {
    e.preventDefault();
    setText(name)
    setName("")
    setStudent((pre) => ({ ...pre, name: name }));
  }
  const handle_chage_name = (event) => {
    setName(event.target.value)

  }
  const handle_toggle_student = () => {
    setCheck((pre) => !pre);
  }




  const handle_add = () => {
    setList_dv((pre) => {
      const dssv = [...pre, { name: name, old: 3 }]
      localStorage.setItem("list_sinhvien", JSON.stringify(dssv));
      setName("");
      return dssv;
    })


  };



return (
  <div>
    <h2>LearnReactjs</h2>
    <h1>{x}</h1>
    <h1>name: {text}</h1>
    <h1>
      ho va ten: {student["name"]}, tuoi: {student.old}
    </h1>
    <button onClick={handle_increase}>increase</button>
    <button onClick={handle_Changetext}>Change</button>
    <form onSubmit={handle_Changetext}>
      <input type="text" placeholder='name' value={name} onChange={handle_chage_name} />

    </form>
    <button onClick={handle_toggle_student}>Toggle</button>
    {check ? <Studentlist /> : ""}

    <ul>
      {list.map((st, key) => {
        return <li>{st}</li>
      })}
    </ul>

    <ul>
      {list_dv.map((st, key) => {
        return <li> {st.name}  {st.old} tuoi
        </li>
      })}
    </ul>

    <form onSubmit={handle_Changetext}>
      <input type="text" placeholder='name' value={name} onChange={handle_chage_name} />

    </form>
    <button onClick={handle_add}>
      Add student
    </button>
  </div>
);

    }
export default App;
    