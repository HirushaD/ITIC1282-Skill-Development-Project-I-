# LankaVoice  
	• Software Stack: DistilBERT + ONNX + Gradio  
	• Technical Depth: ⭐️⭐️⭐️⭐️⭐️

**LankaVoice** is the more structured, modular alternative. Where VidyalayaAI uses one big LLM, LankaVoice builds **five independent tools** that each solve a specific NLP problem

```
1. Language Detection     → Is this text Sinhala, Tamil, English, or code-mixed?
2. Sentiment Analysis     → Positive / Negative / Neutral for Sinhala text
3. Text Summarisation     → Extractive summarisation for Sri Lankan news articles
4. Spell Checker          → Rule-based + dictionary for Sinhala
5. Fake News Classifier   → Binary classifier for Sri Lankan WhatsApp-style claims
```

Each tool is **standalone**  so your 5 students can each own one tool, integrate on Week 7-8, demo together in Week 9-10.  
  
## **Technical Stack:**  
- Python + HuggingFace Transformers (DistilBERT base)  
- ONNX Runtime (quantisation for CPU inference)  
- Gradio UI with tabs for each tool  
- SQLite word dictionary for spell checker  
- Scraped Sri Lankan news + WhatsApp fact-check datasets  
  
## **Why LankaVoice Over VidyalayaAI?**  
  
LankaVoice is **more achievable** each component is an independent, solved ML problem (classification, summarisation) rather than LLM fine-tuning. Better if your team is stronger in classical ML than deep learning. It also produces **five demo-able outputs** on demo day vs. one