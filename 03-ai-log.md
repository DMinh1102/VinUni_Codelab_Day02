# 03 - AI Log and Reflection

## What I used AI for

I used an AI assistant as a product-scoping partner to organize the five member briefs into an opportunity scan, compare candidate quick cards, and draft a bounded deep dive for the Xanh SM charging co-pilot. I also used it to sharpen the prototype contract: JSON fields, a critical-battery escalation rule, human approval, and a manual fallback.

## What needed correction or skepticism

The initial problem descriptions invite assumptions about how dispatchers work and how long each step takes. Those details were not supplied as company evidence. I kept workflow times explicitly labeled as discovery hypotheses and left business impact unquantified rather than inventing company statistics. The proposed success metrics are pilot targets, not claims about current performance.

A model-written station suggestion would also be unsafe if it silently assumed that station status, compatibility, route distance, or queue data were current. I narrowed the prototype so it only drafts from facts included in the input. Missing or stale data requires human review; critical battery below 5% must not result in a station recommendation. Even a well-formed JSON response is not evidence that the recommendation is factually correct.

## Prototype test status

The local environment did not have `GEMINI_API_KEY` or `GOOGLE_API_KEY` configured during this work. The script therefore supports an explicitly labeled offline boundary-check mode so its deterministic safety assertions can run without an API call. Those offline fixtures do **not** show that Gemini passed the tests. Live Gemini behavior still needs to be tested with an authorized key, recorded outputs, and human review.

## Reflection

AI helped me move from a broad list of member ideas to a testable, narrow workflow and made the operational boundaries easier to express. Its main weakness in this task was the temptation to make a polished workflow sound like a verified one. I addressed that by separating supplied facts, assumptions, and pilot targets, and by keeping real-time recommendations and execution out of scope until data and operator evidence exist. My next step is to interview a dispatcher, measure a small baseline, and test the prompt against labeled, de-identified cases before making any production recommendation.
