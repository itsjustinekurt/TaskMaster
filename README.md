import { useState } from "react";
import "./App.css";

function App() {
  // -----------------------
  // STATE VARIABLES
  // -----------------------
  const [inputValue, setInputValue] = useState(""); // stores what the user types
  const [tasks, setTasks] = useState([]);           // stores the list of tasks

  // -----------------------
  // FUNCTIONS
  // -----------------------
  const addTask = () => {
    if (inputValue.trim() === "") return;
    setTasks([...tasks, inputValue]);
    setInputValue("");
  };

  const deleteTask = (indexToDelete) => {
    setTasks(tasks.filter((_, index) => index !== indexToDelete));
  };

  // -----------------------
  // RETURN JSX
  // -----------------------
  return (
    <div className="min-h-screen bg-gray-100 flex items-center justify-center">
      <div className="bg-white p-6 rounded-lg shadow-md w-full max-w-md">
        <h1 className="text-2xl font-bold text-center mb-4">TaskMaster</h1>
        
        {/* Input and Add Button */}
        <div className="flex gap-2 mb-4">
          <input
            type="text"
            value={inputValue}
            onChange={(e) => setInputValue(e.target.value)}
            onKeyDown={(e) => { if (e.key === "Enter") addTask(); }}
            placeholder="Enter a task..."
            className="flex-1 border rounded px-3 py-2"
          />
          <button className="bg-blue-500 text-white px-4 py-2 rounded hover:bg-blue-600" onClick={addTask}>
            Add
          </button>
        </div>
        
        {/* Task List */}
        <ul className="space-y-2">
          {tasks.map((task, index) => (
            <li key={index} className="flex justify-between items-center bg-gray-200 px-3 py-2 rounded">
              <span>{task}</span>
              <button className="text-red-500 font-bold hover:text-red-700" onClick={() => deleteTask(index)}>X</button>
            </li>
          ))}
        </ul>
        
        {/* Task Count */}
        <p className="text-center text-sm text-gray-600 mt-4">
          You have {tasks.length} pending task{tasks.length !== 1 ? "s" : ""}.
        </p>
      </div>
    </div>
  );
}

export default App;
