# LangGraph Retrieval & Validation Workflow

## 📌 Overview

This  basic information validation project implements a simple **LangGraph workflow** that retrieves information from documents, evaluates its relevance, and produces a final response based on the quality of the retrieved data.

The system ensures that only meaningful and relevant answers are processed further, improving reliability in retrieval-based applications.

---

## ⚙️ Workflow Steps

### 1. Start

* The workflow begins with a user query.

### 2. Retrieve Info (`retrieve_info`)

* The query is passed to a retriever.
* The retriever searches a document store and returns relevant context.

### 3. Opinion on Info (`opinion_on_info`)

* The retrieved context and original query are sent to a language model.
* The model evaluates:

  * Whether the information answers the query
  * Whether the context is relevant and sufficient

---

## 🔀 Decision Branching

Based on the model’s evaluation:

### ✅ Positive Opinion (`positive_opinion`)

* The retrieved information is **relevant and useful**
* The system:

  * Accepts the answer
  * (Optional) Summarizes the information
  * Returns a **positive response**

### ❌ Negative Opinion (`negative_opinion`)

* The retrieved information is:

  * Irrelevant, OR
  * Incomplete, OR
  * Does not contain the answer
* The system returns:

  * A **negative response**
  * Explanation such as:

    * "The answer is not relevant to the question"
    * "The required information is not present in the context"

---

## 🔚 End (`__end__`)

* Both positive and negative branches converge here.
* Final output is returned to the user.

---

## 🧠 Workflow Diagram

<img width="362" height="432" alt="image" src="https://github.com/user-attachments/assets/356c0f97-1818-464e-890f-bf3eb940c591" />



## 📤 Output Behavior

| Scenario              | Output                                     |
| --------------------- | ------------------------------------------ |
| Relevant answer found | Positive response (optionally summarized)  |
| Irrelevant answer     | Negative response with explanation         |
| No answer in context  | "Answer not found in the provided "
