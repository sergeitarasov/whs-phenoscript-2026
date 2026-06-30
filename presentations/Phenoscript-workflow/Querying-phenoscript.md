---
marp: true
theme: default
paginate: true
html: true
style: |
  section { font-size: 1.3rem; }
  h1 { color: #2c5f8a; }
  h2 { color: #2c5f8a; }
  h3 { color: #2c5f8a; }
  code { background: #f0f4f8; border-radius: 3px; padding: 0 4px; }
  pre { font-size: 0.8rem; }
  table { font-size: 1.1rem; }
  .columns { display: grid; grid-template-columns: 1fr 1fr; gap: 2rem; }
  .note { background: #f0f8ff; border-left: 4px solid #2c5f8a; padding: 0.5rem 1rem; margin-top: 1rem; font-size: 1.1rem; }
---

<div style="display:flex; align-items:center; justify-content:space-between; height:80%; gap:2rem">
<div style="flex:1">

# Querying Phenoscript Descriptions 


<br>

WHS Methodological Pills

**Sergei Tarasov**
[www.tarasovlab.com](https://www.tarasovlab.com)

</div>
<div style="flex:0 0 230px; text-align:center">

![w:120](../../icons/images.png)

![w:120](../../icons/phenoscript.png)

</div>
</div>

---

# PhenoScript-GPT

👉 [chatgpt.com/g/…/phenoscript-gpt](https://chatgpt.com/g/g-69d8e94a33e88191ac4dc13189a27606-phenoscript-gpt)

A custom GPT trained on Phenoscript syntax, ontology rules, and the Annotation Guide.

- **Translate** a textual description into Phenoscript
- **Suggest** ontology terms for structures and qualities
- **Debug** inconsistencies — paste your Phenoscript and ask what is wrong

<div class="note">
⚠️ Like all LLMs, it can occasionally hallucinate ontology terms.
</div>





---

# Querying Descriptions — Sparklis

Once the knowledge base is built, query it with **Sparklis** — a visual SPARQL interface that requires no SPARQL knowledge.

**To open:** right-click `output/kb/<projectname>-kb.ttl` → **Phenoscript: Browse with Sparklis**

<br>

![w:850](img/sparklis.png)

---

# Sparklis — Example Query

Query: *"Show all coloured body parts and the species they belong to"*

![w:900](img/sparlis-query.png)

<br>

📎 [Sparklis example queries](https://www.irisa.fr/LIS/ferre/sparklis/examples.html)

---

# Step 3 — Submit *(Experimental)*

Once SHACL says `Conforms` and the reasoner says `Success`, click **Prepare for Submission**.

The extension checks both conditions and creates a `.zip` in `submit/` containing all `.yphs` files and `phs-config.yaml`.

<br>

### How to Submit

> ⚠️ Submitted data will be **publicly accessible**.

1. Name your file: `<FamilyName>_<SurnameInitial>.zip` — e.g., `Scarabaeinae_SmithA.zip`
2. Upload via the **[Submission Form](https://docs.google.com/forms/d/e/1FAIpQLScARO6AdiNZu7Uh_dM0XVwEYuxwwRA8hviEH4UJ1fERjkZPkA/viewform)**

Your file will be uploaded to **[insectKG100](https://github.com/sergeitarasov/insectKG100-repo)**, where the full pipeline will run automatically across all submitted descriptions.

