# Invisor: case study

Invisor is an AI product that helps real-estate investors filter and underwrite acquisitions. I design, build and run it myself. Live at [app.invisor.es](https://app.invisor.es).

This repo is a write-up only. The code is private.

## The problem

An investor looking for assets to buy, refurbish or rent scrolls through hundreds of portal listings and builds a spreadsheet for each candidate. Most fail a basic return check, but finding that out takes hours. Invisor does that first financial filter.

It does not replace legal checks such as charges, occupancy or change of use. The product tells the user to verify those.

## What the user gets

1. The investor writes a thesis: location, asset type, strategy, target yield, budget.
2. Invisor researches the market against that thesis.
3. Each asset lands in one of three buckets: buy, study or discard, with a score and the numbers behind it, including exit price and maximum offer.
4. Assets priced far below the automated valuation go to "study", not "buy". A big discount is more often a hidden problem than a bargain.

## My role

Everything: product, UX, frontend, backend, AI, data, deployment, sales demos. No team.

## How it is built (at concept level)

- **A research agent built as a graph.** The Researcher is not one prompt. It is a graph of specialised agents that plan, search, extract and check each other's work, so each step stays small and testable.
- **A model router.** Each request is routed to the model and reasoning effort that best balance quality, speed and cost, instead of sending everything to one expensive model. I use Jev Router by TypeSafe for this.
- **ML next to the LLMs.** Valuation and scoring use machine-learning models in a separate AI service. LLMs read and reason over unstructured listings; statistical models handle the numbers.
- **Scraping with workers.** Data collection runs as background workers, separate from the web app, because a market run takes far longer than a web request.
- **Self-serve onboarding.** An investor signs up, writes a thesis and gets a first analysis without talking to me.

Stack at a glance: React and TypeScript front end, Python services on Google Cloud, Postgres on Supabase for data and auth.

I keep the internals private on purpose. The interesting part of the product is how these pieces fit together, not which libraries they use.
