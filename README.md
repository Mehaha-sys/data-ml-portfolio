# Data & Machine Learning Portfolio

I use data analysis and machine learning to explore questions, test assumptions, and understand what information can—and cannot—tell us.

This portfolio brings together projects in predictive modeling, performance analysis, and data processing. Each project starts with a question and works toward an evidence-based answer through data preparation, exploratory analysis, statistical methods, or machine learning.

## How I Approach Data

For me, working with data is not just about producing a model or a visualization. It is about understanding the problem well enough to decide what to measure, how to evaluate the evidence, and how to interpret the result responsibly.

Across my projects, I aim to:

- Start with a question. Define what I want to understand before choosing a method.
- Understand the data. Examine its structure, quality, limitations, and relevance to the problem.
- Build a reproducible process. Organize analysis into clear steps that can be checked, repeated, and improved.
- Evaluate, rather than assume. Use appropriate metrics and validation to understand how well an approach performs.
- Interpret the results. Connect technical outputs to the original question while being transparent about uncertainty and limitations.

I see each project as an opportunity to improve both my technical skills and my judgment in working with data.

## Projects

### 1. Exoplanet Candidate Classification

**Question**: Can a small number of measurements help distinguish confirmed exoplanets from false-positive candidates?

This project explores classification using measurements associated with Kepler Objects of Interest (KOIs). It examines how a machine learning model can distinguish between two outcomes and investigates which measurements may provide useful predictive information.

The broader goal is to understand whether a simpler, more interpretable set of features can provide useful classification performance—not merely whether a model can achieve a high score.

"Explore the project →" (./exoplanet-candidate-classification/)

### 2. Formula 1 Qualifying Analysis

**Focus**: Building a structured and verifiable process for analyzing Formula 1 qualifying data.

This project approaches racing data as a data-engineering and analysis problem. It emphasizes consistent data preparation, validation, and the calculation of comparable performance metrics across qualifying sessions.

The aim is to make the process behind the analysis as important as the numbers it produces: data should be checked, transformations should be explicit, and comparisons should follow consistent rules.

"Explore the project →" (./f1-qualifying-analysis/)

### 3. Video Game Commercial Performance Analysis

**Question**: What can commercial performance, ratings, gameplay characteristics, and review sentiment tell us about video games?

This project explores relationships between different dimensions of video game data. By bringing commercial indicators together with player and critic ratings, gameplay metrics, and sentiment measures, it investigates how multiple sources of information can be used to study performance.

The central interest is not simply identifying which games perform well, but examining which patterns the data supports and where the limits of those conclusions lie.

"Explore the project →" (./video-game-commercial-performance-analysis/)

## What I’m Developing

Through this work, I am developing my ability to move from an open-ended question to a structured, defensible analysis. That includes working with real-world datasets, designing data workflows, applying statistical and machine learning techniques, evaluating results, and communicating findings clearly.

I am especially interested in the space between building a model and understanding what it actually tells us: which variables matter, how reliable the results are, what assumptions shape the analysis, and whether a simpler approach can answer the question just as well.

These projects represent an ongoing learning process. I aim to document not only the outcomes, but also the reasoning, decisions, and limitations behind them.

## Tools & Methods

Depending on the project, my work involves:

- Languages: Python, SQL where applicable
- Data analysis: Pandas, NumPy
- Machine learning: Scikit-learn and classification workflows
- Analysis practices: Data cleaning, exploratory analysis, feature evaluation, validation, and performance metrics
- Documentation: Notebooks, project READMEs, and dataset documentation

## Repository Structure

Each project has its own directory containing the relevant analysis, supporting data documentation, and project-specific README.

data-ml-portfolio/
├── exoplanet-candidate-classification/
├── f1-qualifying-analysis/
├── video-game-commercial-performance-analysis/
└── README.md

Individual project READMEs explain the research question, data, methodology, results, and limitations in more detail.

---

This portfolio is a record of how I learn to ask better questions, work more carefully with evidence, and turn data into useful understanding.
