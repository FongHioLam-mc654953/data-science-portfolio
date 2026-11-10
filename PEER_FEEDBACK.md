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
| 2.1 | Two charts carry the identical in-figure title | `plt.title('R^2 Using Test Data')` is used for both the polynomial-order chart and the overfitting chart | **Fixed.** Each figure now carries its own title — "Auto: extra polynomial degrees stop buying test accuracy", "Auto: training and validation R² across eight orders of alpha", "Laptops: test R² collapses from degree 2 onward", "King County: sale price against above-ground living area". The duplicated overfitting chart was dropped from the gallery and replaced with the alpha-sweep chart |
| 2.2 | Axis label written as `R^2` and does not say train vs test | `plt.ylabel('R^2')` while the caption states blue = validation, red = training | **Fixed.** Every R² axis now reads `R² (coefficient of determination)`, the training, test and validation series are each named in an in-figure legend, and the same wording is used in the notebooks and the page captions |
| 2.3 | Alpha chart has no log scale, compressing the informative region | Alpha grid spans eight orders of magnitude; no `set_xscale` in the notebook | **Fixed.** The notebook now builds `Alpha = np.logspace(-3, 5, 161)` and the figure uses `ax.set_xscale('log')`; the axis label states the log scale and the range, and the GridSearchCV pick (alpha = 10 000) is drawn as a labelled dashed line |
| 2.4 | Duplicate value in the alpha grid | `100000` appears twice in `parameters1` | **Fixed.** `parameters1` and `parameters2` now both read `[0.001, 0.1, 1, 10, 100, 1000, 10000, 100000]`, and the logged `GridSearchCV` representation in the notebook was regenerated to match |
| 2.5 | Gallery thumbnails are unreadable | Two-column grid inside a 1080 px container gives roughly 500 px per chart | **Fixed.** Every gallery now leads with its key chart at the full card width (about 975 px instead of 500 px); the remaining charts sit two to a row, a chart left on its own takes the full row, and below 860 px every chart is full width. The chart carries the same "click to enlarge" link, so the page now reads as text at normal zoom without opening anything |
| 2.6 | Captions are labels, not takeaways | "R-squared across polynomial orders", "Cross-validation overfitting scores" | Rewrote all `<figcaption>` elements as conclusions, e.g. "Auto: test R² peaks at degree 2 (0.741) then slides to 0.631 by degree 4"; the two captions that described the redrawn Module 05 and Module 06 charts were rewritten again to match the regenerated figures |
| 2.7 | Inconsistent in-figure titles | The Module 06 price-vs-sqft chart has no in-figure title while other charts do | **Fixed.** Both Module 06 charts now carry an in-figure title and unit-bearing axis labels: "King County: sale price against above-ground living area" (square feet vs USD) and "Insurance: charges against BMI, before the smoker split" (kg/m² vs USD) |

### 2.3 Structure — missing sections

| # | Section | Status in the review | Action taken |
| --- | --- | --- | --- |
| 3.1 | Peer feedback and change log | Missing | Created this file and linked it from `README.md` and `index.md` |
| 3.2 | Project-level Key Findings | Missing on the site, present in the repository README | Added a three-bullet **Key Findings** block to both `index.md` and the Project Overview card in `index.html` |
| 3.3 | Limitations / future work | Missing on the site, present in the repository README | Added a four-bullet **Limitations** block to both `index.md` and the Project Overview card |
| 3.4 | Dataset provenance | Links only, no dataset shape | Added a **Datasets** line naming the four sources (UCI Automobile, UCI Laptops Pricing, Kaggle King County House Sales, Kaggle Medical Insurance Cost) and their educational use |
| 3.5 | Top navigation / anchor menu | Only footer anchors existed | **Fixed.** Added a sticky top bar with links to About, Skills, Projects, Overview, Module 01–06, Preliminary and the repository. In-page links scroll smoothly, `scroll-margin-top` keeps each heading clear of the bar, the bar scrolls sideways instead of wrapping on narrow screens, and the section currently on screen is highlighted and kept in view |
| 3.6 | Course and date context | Missing, so a grader cannot tell course or term | Added "CISC7204 Machine Learning · November 2026" to the hero badge, the Project Overview status line, and the About list in `index.md` |
| 3.7 | Attribution for the pair project | The Preliminary Project is a pair project but the site gave no attribution | Added an **Attribution** note to the Preliminary Project card and marked the project as a pair project in `index.md` |
| 3.8 | CV / LinkedIn link | Missing, described as optional | **Fixed for CV, closed for LinkedIn.** The CV is now published with the site as `assets/cv/FONG_HIO_LAM_CV.pdf` and linked as "View CV (PDF)" from the About section and the footer of `index.html` (and from the About list in `index.md`), opening in a new tab. No LinkedIn profile is listed, because none exists — this is the final position on that half of the item, not a pending task |

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
| 15 | Re-ran the Module 05 and Module 06 figures with per-figure titles, R² axis labels that name the series, a log alpha axis, no duplicated alpha value and in-figure titles on the Module 06 charts, then re-exported the PNGs into `images/` | 2.1, 2.2, 2.3, 2.4, 2.7 | `Module 05/Module05_Lab01_*.ipynb`, `Module 05/Module05_Lab02_*.ipynb`, `Module 06/Module06_*.ipynb`, `images/*.png` | `782a9a7` (notebooks), `80b6e14` (images) |
| 16 | Replaced the duplicated overfitting chart in the Module 05 gallery with the alpha-sweep chart and rewrote the two Module 06 captions so they describe the redrawn charts | 2.1, 2.6 | `index.html` | `80b6e14` |
| 17 | Promoted the first chart of every gallery to the full card width so its tick labels and legends are readable without clicking; the remaining charts sit two to a row, a leftover chart fills the row, and every chart is full width below 860 px | 2.5 | `index.html`, `assets/css/style.css` | b4935ab |
| 18 | Added a sticky top navigation bar with in-page links to About, Skills, Projects, Overview, Module 01–06, Preliminary and the repository, plus smooth scrolling, a `scroll-margin-top` offset so headings clear the bar, a horizontally scrolling link row on narrow screens and current-section highlighting | 3.5 | `index.html`, `assets/css/style.css` | b4935ab |

### 3.1 Deferred and open items

| Item | Reason |
| --- | --- |
| 2.1, 2.2, 2.3, 2.4, 2.7 — in-figure titles, axis labels, log scale, duplicate alpha, missing title | **Closed.** The four notebooks were edited, their figures re-rendered and the exported PNGs in `images/` replaced; the gallery and the captions were updated in the same change. |
| 2.5 — gallery thumbnails about 500 px wide | **Closed.** Addressed in the layout pass recorded as change 17: the key chart of every gallery now spans the full card width, the remaining charts sit two to a row, a leftover chart fills the row, and every chart goes full width on narrow screens. |
| 3.5 — top navigation | **Closed.** Addressed in the same pass, recorded as change 18: a sticky top bar with smooth-scrolling anchors, a scroll offset for the headings, a horizontally scrolling link row on narrow screens and current-section highlighting. |
| 3.8 — CV / LinkedIn link | **Closed.** The CV was copied unchanged into the site as `assets/cv/FONG_HIO_LAM_CV.pdf` and is linked as "View CV (PDF)" from the About section and the footer of `index.html` and from the About list in `index.md`, opening in a new tab. No LinkedIn profile is offered: there is no public profile to link, and this is the final decision on that part of the item rather than an outstanding task. |
| 4.4 — contact address vs GitHub handle | **Closed, no action needed.** Both values were confirmed correct by the student: the five-digit form is the university mail account and the six-digit form is the student ID used in the GitHub handle. The mismatch reported in the review is by design rather than a typo. |

---

## 4. Rubric self-check

Scored against the six criteria in the assignment brief. Each entry records the level I would defend, the artefact that supports it, and what is still missing, so that a grader can check the claim rather than take it on trust.

| Criterion | Weight | Self-assessed level | Evidence | Remaining gap |
| --- | --- | --- | --- | --- |
| **Project Repository** | 15 | Strong | Public repository `FongHioLam-mc654953/data-science-project` organised as `Module 01`–`Module 06` plus `PreliminaryProject_Pair`; every module holds its notebooks, its CSV data and its exported figures; student identifiers were stripped from filenames and notebooks before publication. Each notebook is linked directly from its card in `index.html` and from `index.md` | No `LICENSE` file and no `requirements.txt` / environment file in the project repository, so a reader cannot pin the library versions or see the reuse terms |
| **README Documentation** | 25 | Adequate | `README.md` states the repository's purpose, its contents (homepage, project showcase, peer-review record) and points to `index.md`; `index.md` carries the four research questions, the shared approach, three interpreted key findings, four limitations, dataset provenance and per-module notebook/data/figure links | `README.md` itself is still 19 lines: no dataset descriptions, no how-to-run section, no requirements list and no dataset licence note. The substance sits in `index.md` (rendered as the site), so a grader reading only the README sees far less than the work contains |
| **Analysis & Visualizations** | 20 | Strong | One six-stage pipeline (import → cleaning → EDA → modelling → CV/tuning → evaluation) applied to four price datasets; k-fold cross-validation, Ridge regression and `GridSearchCV` over an alpha grid from 0.001 to 100 000; fourteen charts in `images/` with conclusion-style captions and click-to-enlarge, in-figure titles that name the series, R² axis labels, and a log-scale alpha sweep | No Lasso result and no naive-baseline (mean predictor) comparison table in the notebooks; feature engineering stops at dummy variables and binning, so the modelling story is regularisation-only |
| **Content Presentation** | 15 | Strong | Single-page responsive site: sticky section navigation with smooth scrolling, a `scroll-margin-top` offset and current-section highlighting; About / Technical Skills / Projects (Project Overview, Module 01–06, Preliminary) / Reflection / footer; each gallery leads with its key chart at full card width so the axis labels are legible without clicking; layout checked at 1440, 1280, 1024, 768 and 390 px widths | The sticky bar itself needs horizontal scrolling below roughly 1040 px, and no section-level print stylesheet exists, so a printed copy loses the card framing |
| **GitHub Pages Deployment** | 15 | Strong | Live at https://fonghiolam-mc654953.github.io/data-science-portfolio/, published from `main`; after each push the home page was re-checked and returned HTTP 200, and `assets/cv/FONG_HIO_LAM_CV.pdf` returned HTTP 200 | Served by the default Pages build with no custom domain and no post-deploy build check beyond an HTTP status and content probe |
| **Submission & Reflection** | 10 | Strong | This file: reviewer named and dated, every feedback item answered in place, a change log that ties each change to a commit SHA, and a decision on every item including the ones closed without action. A first-person Reflection of about 210 words appears on the site (`#reflection` in `index.html`) and in `index.md`, covering the skills shown, four specific limitations and four concrete next steps. This self-check completes the submission record | The reflection reports the shortcomings but cannot show that the proposed fixes (repeated cross-validation, wider alpha grid, single reproducible pipeline) have been carried out; they remain plans |

**Overall self-assessment: Strong on repository, analysis, presentation and deployment; Adequate on README documentation; the reflection is written and one step short of demonstrated.** The two gaps I would fix first are the thin `README.md` and the missing `requirements.txt` / `LICENSE` in the project repository, because both are cheap and both affect how quickly a grader can reproduce the work.

---

## 5. Conclusion

The review was accurate on every point I could verify: the analysis was already sound, but the portfolio presented it as a sequence of stages and left the research question, the interpretation of the numbers and the limitations off the page entirely. The changes recorded above address the narrative gap — the site now opens with the question, the approach, three interpreted findings and four limitations, and every chart caption states what the chart shows rather than what it plots. The metadata and disclaimer defects are gone.

The notebook figures were rebuilt in the second pass: the four notebooks now name every series, title every chart, plot the alpha sweep on a log axis and carry a de-duplicated hyperparameter grid, and the exported PNGs in `images/` were regenerated from those runs. The duplicated overfitting chart is gone, so no two figures can be mistaken for one another any more. The third pass closed the two presentational items: each gallery now opens with its key chart at the full card width, so the axis labels are legible without clicking, and the page carries a sticky section navigation that scrolls smoothly and highlights where the reader is. Only the optional CV and LinkedIn links (3.8) remained open at that point. The fourth pass closes that item: the course CV is published unchanged as `assets/cv/FONG_HIO_LAM_CV.pdf` and linked as "View CV (PDF)" from the About section and the footer, the site and `index.md` carry a first-person Reflection, and this file now ends with a rubric self-check. LinkedIn stays closed rather than pending, because there is no profile to link. No feedback item is outstanding. The contact-address item (4.4) is closed: both identifiers were confirmed correct, so nothing needed changing.

I thank the reviewer for a review that was specific enough to act on: every item above could be mapped to a concrete edit and a commit.