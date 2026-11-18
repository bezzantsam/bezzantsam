# Chrome.ai | Buoy 10 Chinook research

**Sam Bezzant · Applied machine learning and data engineering**

At Buoy 10 on the Columbia River, anglers already know that the time of season matters. I built Chrome.ai to test a narrower question. Seven days before a fishing date, can information available then improve an estimate of retained Chinook per sampled angler over a simple seasonal baseline?

[Explore the research site](https://chrome-ai-research.vercel.app/research) · [See the sources and sampling method](https://chrome-ai-research.vercel.app/sources)

## Defining a measurable outcome

A Washington creel survey records how many anglers were sampled and how many Chinook they retained. I use both counts. A sample of 100 anglers carries more weight in a pooled catch rate than a sample of ten. Missing survey days stay missing. Oregon reports can include encounters with released fish, so I evaluate that outcome separately. This keeps changes in sampling or reporting from looking like changes in fishing conditions.

## Testing a model an angler could have used

I compare a seasonal baseline with a regularized regression model. For each historical test year, the model trains only on earlier years. Both methods are scored on the same fishing dates using mean absolute error, expressed in retained fish per sampled angler. Looking at each year separately helps show whether one unusual season drives the overall comparison.

A tide prediction can be available a week ahead. A river observation recorded on the fishing day arrives too late for that forecast, even when it explains the catch well in hindsight. I use the forecast issue date to decide which inputs are eligible.

## Building a record that can be checked later

The pipeline captures official source files on a schedule and fingerprints the original bytes. That preserves the version used even when an agency revises its report. A monitor checks for missed scheduled runs. I also tested recovery by restoring a private database backup in an isolated PostgreSQL instance and checking that expected source captures were present.

## What someone can inspect today

The public site walks through the target, the baseline, the historical test design, and the source definitions. Numerical research results and forecast values remain private. The August 2027 experiment is frozen in advance. Its seven-day forecasts can be scored against subsequent official observations once those outcomes exist.

[Read the study design](https://chrome-ai-research.vercel.app/research)
