# IA (Groq) — Chat e Transcrição

Variáveis:
```
GROQ_API_KEY=
GROQ_TEXT_MODEL=llama-3.1-70b-versatile
GROQ_STT_MODEL=whisper-large-v3
```

Exemplos em `lib/ai/groq.ts`, `/api/meet/transcribe`, `/api/meet/ingest`.
- Chat: `groq.chat.completions.create({ model, messages })`
- STT: `groq.audio.transcriptions.create({ file, model })`

Pipeline de ATA: transcrever → resumir/decisões → criar tarefas (Kanban).
