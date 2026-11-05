# Peer Review Feedback and Change Log

| Field | Value |
| --- | --- |
| **Reviewer** | Fong Chin Wai (mc653748) |
| **Reviewer role** | Classmate, peer reviewer (CISC7204) |
| **Review date** | 2026-11-05 |
| **Reviewed work** | FONG HIO LAM — CISC7204 Assignment 1 (Build Your GitHub DS Portfolio) |
| **Portfolio** | https://fonghiolam-mc654953.github.io/data-science-portfolio/ |
| **Project repository** | https://github.com/FongHioLam-mc654953/data-science-project |
| **Course context** | CISC7204 Machine Learning · November 2026 |
| **Review scope** | Clarity of the research question, presentation of findings, visualisation readability, missing project-level sections, concrete defects |

This document records the review I received, what I changed in response, and the commit in which each change landed. Items I did not act on are listed separately with the reason, so that the record is complete rather than selective.

---

## 1. Strengths noted by the reviewer

- Clean, responsive single-page site with a clear hero / about / skills / projects / footer flow.
- Consistent structure across the module cards: each one links its notebook, its data and its charts.
- Fourteen charts with captions and click-to-enlarge, which makes the work inspectable rather than decorative.
- The underlying analysis is sound: the pipeline, cross-validation and Ridge tuning are all present and correctly reported.

The reviewer's overall judgement was that the craft is good and that the gap is narrative, not polish — the site read as a log of stages rather than as a project with a question and an answer.

---

## 2. Detailed feedback and response

### 2.1 Clarity — research question, approach, findings

| # | Issue raised | Evidence given | Action taken |
| --- | --- | --- | --- |
| 1.1 | No research question appears on the site | Cards only contain short descriptions such as "Load and inspect the car datasets…"; the four research questions existed only in the repository README | Added a **Research Questions** section to `index.md` and a **Project Overview** card at the top of `#projects` in `index.html`, listing RQ1–RQ4 (car price, laptop price, King County house price, medical insurance charges) |
| 1.2 | Findings are buried inside paragraph prose | The Module 05 card packed six R-squared values and two alpha values into one dense paragraph | Split that paragraph into three interpreted bullets: cross-validation, the overfitting result, and Ridge plus tuning |
| 1.3 | The most interesting result is left unexplained | "4-fold CV mean R-squared 0.522 (±0.291)" — a ±0.291 spread on a mean of 0.522 means a very unstable model, and nothing on the page said so | Added an explicit sentence: the spread measures how strongly the folds disagree, so the model is highly unstable and a single train/test split would have hidden it |
| 1.4 | "Test R-squared = −29.87" reads like a bug | Module 05 card | Added a clause explaining that a negative R-squared means the model performs worse than predicting the mean, which is precisely the overfitting evidence rather than a numerical error |
| 1.5 | Units and currency are never stated | `plt.xlabel('Price (in dollars)')` exists in the notebook, but the page never states the currency | Stated USD once per price project (Modules 01, 04, 05, 06), in the Projects introduction, and in the portfolio-level Approach section |
| 1.6 | No "why this matters" framing | Nothing connected the modules into a single claim | Added a short project abstract and a **Key Findings** block (three bullets with concrete metrics), plus **Approach** and **Limitations** sections |

### 2.2 Visualizations — readability, titles, axis labels, units

| # | Issue raised | Evidence given | Action taken |
| --- | --- | --- | --- |
| 2.1 | Two charts carry the identical in-figure title | `plt.title('R^2 Using Test Data')` is used for both the polynomial-order chart and the overfitting chart | Not actioned — the title lives inside the exported PNG, so it requires re-running the notebook and regenerating the figure; recorded below as deferred |
| 2.2 | Axis label written as `R^2` and does not say train vs test | `plt.ylabel('R^2')` while the caption states blue = validation, red = training | Not actioned — same reason (in-figure axis label) |
| 2.3 | Alpha chart has no log scale, compressing the informative region | Alpha grid spans eight orders of magnitude; no `set_xscale` in the notebook | Not actioned — same reason |
| 2.4 | Duplicate value in the alpha grid | `100000` appears twice in `parameters1` | Not actioned — notebook-level code cleanup, tracked as deferred |
| 2.5 | Gallery thumbnails are unreadable | Two-column grid inside a 1080 px container gives roughly 500 px per chart | Not actioned — requires a layout change to promote one chart to full width |
| 2.6 | Captions are labels, not takeaways | "R-squared across polynomial orders", "Cross-validation overfitting scores" | Rewrote all fourteen `<figcaption>` elements as conclusions, e.g. "Test R-squared turns negative beyond degree 3 — the polynomial memorises the training set instead of learning the trend" |
| 2.7 | Inconsistent in-figure titles | The Module 06 price-vs-sqft chart has no in-figure title while other charts do | Not actioned — in-figure title issue, deferred with 2.1–2.4 |

### 2.3 Structure — missing sections

| # | Section | Status in the review | Action taken |
| --- | --- | --- | --- |
| 3.1 | Peer feedback and change log | Missing | Created this file and linked it from `README.md` and `index.md` |
| 3.2 | Project-level Key Findings | Missing on the site, present in the repository README | Added a three-bullet **Key Findings** block to both `index.md` and the Project Overview card in `index.html` |
| 3.3 | Limitations / future work | Missing on the site, present in the repository README | Added a four-bullet **Limitations** block to both `index.md` and the Project Overview card |
| 3.4 | Dataset provenance | Links only, no dataset shape | Added a **Datasets** line naming the four sources (UCI Automobile, UCI Laptops Pricing, Kaggle King County House Sales, Kaggle Medical Insurance Cost) and their educational use |
| 3.5 | Top navigation / anchor menu | Only footer anchors existed | Not actioned — deferred, see below |
| 3.6 | Course and date context | Missing, so a grader cannot tell course or term | Added "CISC7204 Machine Learning · November 2026" to the hero badge, the Project Overview status line, and the About list in `index.md` |
| 3.7 | Attribution for the pair project | The Preliminary Project is a pair project but the site gave no attribution | Added an **Attribution** note to the Preliminary Project card and marked the project as a pair project in `index.md` |
| 3.8 | CV / LinkedIn link | Missing, described as optional | Not actioned — no CV file or profile URL is available yet |

### 2.4 Concrete defects

| # | Defect | Action taken |
| --- | --- | --- |
| 4.1 | Generated metadata front matter rendered as a visible table at the top of the repository page | Deleted the metadata header block from both `index.md` and `README.md`; both files now begin with their H1 heading |
| 4.2 | Duplicated AI disclaimer line | Deleted all three occurrences (two at the end of `index.md`, one at the end of `README.md`); no disclaimer line remains in any file |
| 4.3 | Meta description promised NLP and deep learning with no such project on the page | Rewrote the meta description to describe the work that actually exists: price regression on car, laptop, house-price and medical-insurance data, with cross-validation, Ridge regression and GridSearchCV |
| 4.4 | Contact address uses five digits (mc65495) while the GitHub handle uses six (mc654953) | Closed as not a defect — both identifiers were confirmed correct: `mc65495` is the university mail account and `mc654953` is the full student ID carried in the GitHub handle. The difference in digit count is intentional, so no contact address was changed |
| 4.5 | Number formatting drifts in Module 06 | Normalised to three decimal places throughout (0.6479 → 0.648), in `index.md` and `index.html` |

### 2.5 Reviewer's strongest single recommendation

The reviewer recommended restructuring from "stages" to "one flagship project": lead with research question, data, approach, key findings, limitations and repository, then keep the module cards below as an implementation appendix.

Action taken: adopted. The Projects section now opens with a **Project Overview** card containing the research questions, approach, key findings, limitations, dataset provenance and status; the six module cards and the Preliminary Project card follow as the implementation walkthrough. The metadata blocks the reviewer flagged were removed in the same change.

---

## 3. Change log

| # | Change | Feedback item | Files | Commit |
| --- | --- | --- | --- | --- |
| 1 | Deleted generated metadata header block and all duplicated disclaimer lines | 4.1, 4.2 | `index.md`, `README.md` | `63cb59c` |
| 2 | Added Research Questions, Approach, Key Findings and Limitations sections | 1.1, 1.6, 3.2, 3.3 | `index.md` | `63cb59c` |
| 3 | Added the Project Overview card at the top of `#projects` | 1.1, 1.6, 3.2, 3.3 | `index.html` | `63cb59c` |
| 4 | Split the Module 05 dense paragraph into three interpreted bullets | 1.2, 1.3, 1.4 | `index.html`, `index.md` | `63cb59c` |
| 5 | Added explanatory sentences for the ±0.291 CV spread and for the negative test R-squared | 1.3, 1.4 | `index.html`, `index.md` | `63cb59c` |
| 6 | Rewrote all fourteen chart captions as takeaway statements | 2.6 | `index.html` | `63cb59c` |
| 7 | Normalised Module 06 metrics to three decimal places | 4.5 | `index.html`, `index.md` | `63cb59c` |
| 8 | Stated USD for every price target and insurance charge | 1.5 | `index.html`, `index.md` | `63cb59c` |
| 9 | Rewrote the meta description to match the projects actually shown | 4.3 | `index.html` | `63cb59c` |
| 10 | Added course and date context (CISC7204, November 2026) | 3.6 | `index.html`, `index.md` | `63cb59c` |
| 11 | Added pair-project attribution to the Preliminary Project | 3.7 | `index.html`, `index.md` | `63cb59c` |
| 12 | Added dataset provenance for the four datasets | 3.4 | `index.html` | `63cb59c` |
| 13 | Created this feedback and change-log file and linked it from the repository README and the portfolio index | 3.1 | `PEER_FEEDBACK.md`, `README.md`, `index.md` | `63cb59c` |
| 14 | Removed the generated metadata block and disclaimer text that had leaked into this file, and closed the identifier question | 4.1, 4.2, 4.4 | `PEER_FEEDBACK.md` | `28b051c` |

### 3.1 Deferred and open items

| Item | Reason |
| --- | --- |
| 2.1, 2.2, 2.3, 2.4, 2.7 — in-figure titles, axis labels, log scale, duplicate alpha, missing title | These are properties of the exported PNGs, not of the page. Fixing them means editing and re-running the Module 05 and Module 06 notebooks, regenerating the figures and re-exporting them into `images/`. Tracked as the next piece of work rather than rushed into this content revision. |
| 2.5 — gallery thumbnails about 500 px wide | Requires a layout change (promoting the overfitting chart to full width above a smaller gallery). Deferred so that the structural content fixes could be reviewed first. |
| 3.5 — top navigation | Requires new markup and responsive styling; deferred to the same layout pass as 2.5. |
| 3.8 — CV / LinkedIn link | No CV document or public profile URL is available to link yet. |
| 4.4 — contact address vs GitHub handle | **Closed, no action needed.** Both values were confirmed correct by the student: the five-digit form is the university mail account and the six-digit form is the student ID used in the GitHub handle. The mismatch reported in the review is by design rather than a typo. |

---

## 4. Conclusion

The review was accurate on every point I could verify: the analysis was already sound, but the portfolio presented it as a sequence of stages and left the research question, the interpretation of the numbers and the limitations off the page entirely. The changes recorded above address the narrative gap — the site now opens with the question, the approach, three interpreted findings and four limitations, and every chart caption states what the chart shows rather than what it plots. The metadata and disclaimer defects are gone.

The remaining work is concentrated in one place: the notebook figures themselves (deferred items 2.1–2.4 and 2.7) and the page layout that presents them (2.5, 3.5). Both will be handled in the next revision. The contact-address item (4.4) is now closed: both identifiers were confirmed correct, so nothing needed changing.

I thank the reviewer for a review that was specific enough to act on: every item above could be mapped to a concrete edit and a commit.