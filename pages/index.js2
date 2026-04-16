import { useState } from "react";

export default function Home() {
  const [input, setInput] = useState("");
  const [messages, setMessages] = useState([]);

  const sendMessage = async () => {
    if (!input) return;

    const text = input;
    setInput("");

    setMessages((m) => [...m, { role: "user", text }]);

    const res = await fetch(
      "https://ai-hub-backend-qci4.onrender.com/chat",
      {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({ message: text }),
      }
    );

    const data = await res.json();

    setMessages((m) => [...m, { role: "ai", text: data.reply }]);
  };

  return (
    <div style={{ maxWidth: 600, margin: "0 auto", padding: 20 }}>
      <h2>AI Hub</h2>

      <div style={{ minHeight: 400, border: "1px solid #ccc", padding: 10 }}>
        {messages.map((m, i) => (
          <p key={i}>
            <b>{m.role === "user" ? "Du" : "AI"}:</b> {m.text}
          </p>
        ))}
      </div>

      <input
        value={input}
        onChange={(e) => setInput(e.target.value)}
        style={{ width: "80%", marginTop: 10 }}
      />

      <button onClick={sendMessage}>Senden</button>
    </div>
  );
}
