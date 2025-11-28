# 2400031718-EndSemExam1
import React, { useState } from "react";
import { useAsyncList, useReader } from "@react-stately/data";

export default function App() {
  
  const students = useAsyncList(
    async load() {
      // Example static data
      return {
        items: [
          { id: 1, name: "Rahul", present: false },
          { id: 2, name: "Priya", present: false },
          { id: 3, name: "Arjun", present: false },
        ]
      };
    }
  });

  
  const data = useReader(students);

  const toggleAttendance = (id) => {
    students.update(item => item.id === id ? {...item, present: !item.present} : item);
  };

 => s.present).length;

  return (
    <div style={styles.container}>
      <h2>📚 Student Attendance Tracker</h2>
      <ul style={styles.list}>
        {data.items.map(student => (
          <li key={student.id} style={styles.item}>
            <span>{student.name}</span>
            <button
              style={student.present ? styles.presentBtn : styles.absentBtn}
              onClick={() => toggleAttendance(student.id)}
            >
              {student.present ? "Present" : "Absent"}
            </button>
          </li>
        ))}
      </ul>

      <div style={styles.summary}>
        ✅ Present: {totalPresent} / {data.items.length}
      </div>
    </div>
  );
}


const styles = {
  container: { fontFamily: "Arial", padding: "20px" },
  list: { listStyle: "none", padding: 0 },
  item: {
    display: "flex",
    justifyContent: "space-between",
    marginBottom: "10px",
    padding: "10px",
    background: "#f5f5f5",
    borderRadius: "6px"
  },
  presentBtn: {
    padding: "6px 12px",
    background: "green",
    color: "white",
    borderRadius: "4px",
    cursor: "pointer"
  },
  absentBtn: {
    padding: "6px 12px",
    background: "red",
    color: "white",
    borderRadius: "4px",
    cursor: "pointer"
  },
  summary: {
    marginTop: "20px",
    fontWeight: "bold",
    fontSize: "18px"
  }
};
