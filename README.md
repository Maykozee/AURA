# AURA
Aura thinking import React, { useState, useEffect } from "react";

/*
  AURA APP - Full Frontend Prototype
  Features:
  - Loading screen
  - Welcome animation
  - Login / Signup
  - OTP verification (mock)
  - Home feed
  - Hashtag system
  - Options page
*/

export default function App() {
  const [stage, setStage] = useState("loading");
  const [user, setUser] = useState(null);
  const [otp, setOtp] = useState("");
  const [generatedOtp, setGeneratedOtp] = useState("");

  // Loading → Welcome
  useEffect(() => {
    setTimeout(() => setStage("welcome"), 2000);
  }, []);

  // OTP generator
  const generateOTP = () => {
    const code = Math.floor(1000 + Math.random() * 9000).toString();
    setGeneratedOtp(code);
    alert("OTP sent: " + code);
  };

  // LOGIN
  const login = () => {
    setUser({ name: "AURA USER" });
    setStage("home");
  };

  // SIGNUP → OTP
  const signup = () => {
    generateOTP();
    setStage("otp");
  };

  // VERIFY OTP
  const verifyOtp = () => {
    if (otp === generatedOtp) {
      setUser({ name: "NEW USER" });
      setStage("home");
    } else {
      alert("Wrong OTP");
    }
  };

  // ================= LOADING =================
  if (stage === "loading") {
    return (
      <div style={styles.center}>
        <h1 style={styles.logo}>AURA</h1>
        <p>Loading...</p>
      </div>
    );
  }

  // ================= WELCOME =================
  if (stage === "welcome") {
    return (
      <div style={styles.center}>
        <h1 style={styles.bigText}>Welcome to AURA 💫</h1>
        <button style={styles.button} onClick={() => setStage("auth")}>
          Start
        </button>
      </div>
    );
  }

  // ================= AUTH =================
  if (stage === "auth") {
    return (
      <div style={styles.container}>
        <h2>Login</h2>
        <input placeholder="username" style={styles.input} />
        <input placeholder="password" type="password" style={styles.input} />
        <button style={styles.button} onClick={login}>Login</button>

        <hr />

        <h2>Signup</h2>
        <input placeholder="username" style={styles.input} />
        <input placeholder="email" style={styles.input} />
        <input placeholder="password" type="password" style={styles.input} />
        <button style={styles.button} onClick={signup}>Signup</button>
      </div>
    );
  }

  // ================= OTP =================
  if (stage === "otp") {
    return (
      <div style={styles.center}>
        <h2>OTP Verification</h2>
        <input
          placeholder="Enter OTP"
          style={styles.input}
          onChange={(e) => setOtp(e.target.value)}
        />
        <button style={styles.button} onClick={verifyOtp}>
          Verify
        </button>
      </div>
    );
  }

  // ================= HOME =================
  if (stage === "home") {
    return (
      <div>
        <div style={styles.nav}>
          <span>AURA</span>
          <button onClick={() => setStage("options")}>⚙</button>
        </div>

        <div style={styles.feed}>
          <h3>🔥 Trending #Hashtags</h3>
          <p>#love #ethiopia #chat #aura #dating</p>

          <div style={styles.card}>
            <p><b>{user.name}</b> posted</p>
            <p>Welcome to AURA community 💫</p>
          </div>

          <div style={styles.card}>
            <p>#match</p>
            <p>Someone liked your profile ❤️</p>
          </div>
        </div>
      </div>
    );
  }

  // ================= OPTIONS =================
  if (stage === "options") {
    return (
      <div style={styles.container}>
        <h2>Options</h2>

        <button style={styles.button}>Profile</button>
        <button style={styles.button}>Privacy</button>
        <button style={styles.button}>Notifications</button>
        <button style={styles.button}>Premium 💎</button>

        <button style={styles.button} onClick={() => setStage("home")}>
          Back
        </button>
      </div>
    );
  }

  return null;
}

// ================= STYLES =================
const styles = {
  center: {
    height: "100vh",
    display: "flex",
    flexDirection: "column",
    justifyContent: "center",
    alignItems: "center",
    background: "#0f0f1a",
    color: "white",
  },
  container: {
    padding: 20,
    background: "#0f0f1a",
    color: "white",
    minHeight: "100vh",
  },
  logo: {
    fontSize: 40,
    fontWeight: "bold",
  },
  bigText: {
    fontSize: 30,
    animation: "fadeIn 2s",
  },
  input: {
    display: "block",
    margin: "10px 0",
    padding: 10,
    width: "100%",
  },
  button: {
    padding: 10,
    margin: 5,
    background: "#6c5ce7",
    color: "white",
    border: "none",
    cursor: "pointer",
  },
  nav: {
    display: "flex",
    justifyContent: "space-between",
    padding: 15,
    background: "#111",
    color: "white",
  },
  feed: {
    padding: 20,
  },
  card: {
    background: "#1c1c2e",
    padding: 15,
    margin: 10,
    borderRadius: 10,
  },
};
