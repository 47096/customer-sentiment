# What are customers actually saying?

**A voice-of-customer problem, solved with review text.**

Teams read a handful of reviews and argue about “what people think.” I turn **raw customer language** into a clear **positive / negative read** you can use in product, marketing, and ops — without a research team.

---

## The stake

Reviews and tickets are free research — if someone has time to read them. Miss the negative patterns and you fix the wrong things. Squeaky voices dominate. **Silent majority sentiment** is where churn and word-of-mouth actually live.

## The story

You have **1,000 restaurant reviews** with a simple label: liked / not liked. The job is not “build an SVM.” The job is:

> **Can we trust a model to say what customers feel — from free text alone?**

I built a full text pipeline: words → features → classifier → **predictions on brand-new sentences**.

**Outcome on this build:**
- Balanced classes (~50/50), so accuracy is meaningful  
- Model classifies **unseen review text** as positive or negative  
- Same pattern works on **support tickets, app store reviews, NPS verbatims**

> **The commercial idea:** stop sampling five reviews and guessing. Score the corpus. Fix what the negatives are actually about.

---

## What that looks like in your world

| You have | I turn it into |
|----------|----------------|
| Reviews / tickets / verbatims | **Sentiment scores** per comment |
| “People seem unhappy lately” | Counts + examples you can act on |
| Manual tag QA on a sample | **Scalable first-pass** triage for humans |
| Dashboard of stars only | The **language** behind the stars |

**Typical engagement:** we connect your review source → label a sample → train / tune → you get a scored export + the words driving negative sentiment.

**[Talk to me about customer voice →](https://datafying.co/#contactus)** · [datafying](https://datafying.co/)

---

## Why marketing & product leaders bring me in

- Starts from **business language** (“liked / not liked”), not jargon  
- Shows the **text → numbers** step clients never see — so they trust the output  
- Same pattern scales from restaurant reviews to **VoC programs**  
- Honest limits (slang, sarcasm, domain shift) stated up front  

---

## Proof of craft *(technical)*

### Job
Binary classification: `Liked` ∈ {0, 1} from free-text `Review`.

### Pipeline
1. **Vectorise** — `CountVectorizer` (bag-of-words, English stop words dropped)  
2. **Split** — 75/25, stratified  
3. **Train** — SVC (RBF)  
4. **Evaluate** — accuracy on holdout (balanced labels)  
5. **Smoke test** — custom unseen sentences  

### What's in the repo

| File | Role |
|------|------|
| `01-text-features.ipynb` | How words become numbers (unigrams / bigrams) |
| `02-sentiment-model.ipynb` | Full pipeline + predictions on new text |

### Example
```python
unseen_text = vect.transform(["Good customer service! The food was nice"])
model.predict(unseen_text)  # => [1] (positive)
```

### Limits (honesty)
- Binary labels only (no star rating yet)  
- Classic bag-of-words — weak on sarcasm and heavy slang  
- Domain matters: retrain when you switch from restaurants to your product  
- **Human review** still needed for edge cases and root-cause themes  

---

## Reproduce

```bash
git clone https://github.com/47096/customer-sentiment.git
cd customer-sentiment
pip install -r requirements.txt
jupyter notebook 02-sentiment-model.ipynb
```

Or open in Colab from the notebook file (no setup).

**Data:** 1,000 restaurant reviews (`Review` + `Liked`) in `data/`.

**Stack:** `scikit-learn` · `pandas` · `CountVectorizer` · `SVC`

---

## Next step

If reviews are piling up and the team is guessing — that is the engagement I run.

**[Book a conversation →](https://datafying.co/#contactus)** · Customer analytics & voice-of-customer · [datafying](https://datafying.co/)
