# **VidyalayaAI**  
	• Software Stack: Ollama + Fine-tuned LLM + Gradio  
	• Technical Depth: ⭐️⭐️⭐️⭐️⭐️

A rural O/L student in Anuradhapura with no tuition and no internet can put their essay into VidyalayaAI and get the same quality of feedback a Colombo student pays Rs. 2000/session for. This directly addresses **education inequity** a core social problem for Sri Lanka's future.

## Novelty 
	No Sri Lankan student has access to AI writing feedback in Sinhala or Tamil. Existing tools (Grammarly, ChatGPT) are English-only, culturally misaligned, and require internet + cost money. VidyalayaAI solves this by **fine-tuning a small open-source LLM** on Sri Lankan O/L and A/L exam answer scripts and running it **entirely offline on a ordinary laptop** — no API costs, no data leaves the machine.

```
[Student past exam scripts] → [Dataset labeling] → [Fine-tune Mistral/TinyLlama via Ollama]
                                        ↓
[Student submits essay via Gradio UI] → [Local LLM inference] → [Structured feedback report]
                                         ↓
 Content relevance | Structure | Language quality | Keyword coverage
```

## Feasibility Check

**"LLMs need a GPU"**  
	• Reality: Ollama quantised models (Q4) run on laptop CPU at ~5-10 tokens/sec — slow but usable for a demo  
  
**"Fine-tuning needs huge data"**  
	• Reality: LoRA fine-tuning works with 500–1000 annotated samples if using a small model  
  
**"Sinhala NLP is too hard"**  
	• Reality: Start with one exam type (GCE O/L Sinhala Language Paper 2) — narrow scope = achievable