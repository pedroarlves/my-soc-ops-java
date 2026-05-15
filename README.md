🌐 [Português (BR)](README.pt_BR.md) | [Español](README.es.md)

# Soc Ops

A playful social bingo experience for team mixers and icebreakers.

**Connect faster, spark conversations, and celebrate every 5-in-a-row win.**

> Soc Ops turns event icebreakers into a friendly bingo challenge: find people who match the prompts, mark your board, and race for a line.

---

## ✨ Why Soc Ops?

- **Designed for in-person mixers** — a simple web game to help teams meet and mingle.
- **Built with Spring Boot + Thymeleaf** — no heavy frontend framework required.
- **Customizable bingo prompts** — easy to swap in new icebreaker questions.
- **Workshop-ready** — includes guided lab content for learning AI-assisted development.

---

## 🚀 Quick Start

Open a terminal and run:

```bash
cd socops
./mvnw spring-boot:run
```

Then visit: `http://localhost:8080`

---

## 📦 Project Contents

- `socops/` — Java Spring Boot application
- `socops/src/main/java` — backend controllers, service logic, and models
- `socops/src/main/resources/templates` — Thymeleaf UI templates
- `workshop/` — step-by-step learning guides for building the app and agents

---

## 🧪 Build & Test

```bash
cd socops
./mvnw clean package
./mvnw test
```

---

## 📚 Learn with the Lab

The repository includes a guided workshop that walks through:

| Part | Topic |
|------|-------|
| [**00**](workshop/00-overview.md) | Project overview and goals |
| [**01**](workshop/01-setup.md) | Setup and context engineering |
| [**02**](workshop/02-design.md) | Design-first frontend improvements |
| [**03**](workshop/03-quiz-master.md) | Building a custom quiz master agent |
| [**04**](workshop/04-multi-agent.md) | Multi-agent feature development |

> Start with the full guide: [workshop/GUIDE.md](workshop/GUIDE.md)

---

## 🛠️ Prerequisites

- [Java 21 JDK](https://adoptium.net/) or higher
- [Apache Maven 3.9+](https://maven.apache.org/) or use the included Maven Wrapper

---

## 📣 Contribute

Want to add new bingo prompts, improve the UI, or expand the game rules? The workshop and codebase are built to help you iterate quickly.
