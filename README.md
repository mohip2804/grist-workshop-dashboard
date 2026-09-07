# Grist workshop dashboard

A single [Grist](https://www.getgrist.com/) custom widget: standard hours
against actual hours, for a vehicle service workshop.

One file, no build step, no dependencies. It reads three tables — `Jobs`,
`Assignments`, `Operators` — and does every calculation itself, so it does not
depend on formula columns existing in any particular document.

## Using it

In a Grist document: **Add Widget → Custom → Custom URL**, paste this page's
URL, and set access to **Full** (it reads three tables; a widget is scoped to
one otherwise). It never writes.

## What it shows

- **Data health** — how many job cards can actually be measured, so no
  efficiency figure is read without knowing what it was drawn from
- **Cars in the selected period** — standard against actual, colour-coded
- **Technicians** — hours booked, standard hours earned, efficiency
- **Day by day** — bars for hours with an efficiency line on its own axis
- **Months** — click one for its cars and technician ranking

## The rules it applies

- A stint longer than a shift is wall-clock time, not work, and is excluded
- A standard above 24 hours is a data error, not a standard
- A card that is not finished and under a quarter booked has no meaningful
  variance yet
- A car's standard is split between the technicians on it in proportion to the
  hours each booked, so the parts add back to the car's standard rather than
  double-counting it per technician
- Efficiency is a ratio of two sums, never an average of percentages

## Privacy

No hostname, customer, or credential appears in this file. The Grist API is
loaded from whichever instance is showing the widget, determined at runtime.
All data stays in Grist, behind that document's own login — this page holds
none of it.
