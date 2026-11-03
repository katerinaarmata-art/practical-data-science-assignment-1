# LLM interaction record — Assignment 1

## Tools and scope
I used ChatGPT, including its coding tools, for guidance, debugging, notebook
construction, checking results and drafting explanations. I did not record the exact
model version of every earlier chat. I used SynDisco with
Qwen2.5-3B-Instruct-bnb-4bit for the earlier discussion trials and
Qwen2.5-7B-Instruct-bnb-4bit for the final experiment. The notebook records
the actual model path, package versions, prompts, identities, responses and conditions.
I used Claude (claude.ai) only for a post-run review and pasted that review into
my conversation with ChatGPT; see sections 11–13. Qwen2.5-7B remained the experimental
annotation model, and Claude was not an annotator. This record summarises the
exchanges shared in this conversation, rather than providing a verbatim export
of every separate chat.

## 1. Understanding the task and preserving independent ratings
I asked what the assignment requires, how annotators and LLMs work, whether
ChatGPT could know the 20 human ratings, and whether Claude or another
model could be used independently. Guidance distinguished coding assistance from
the separate model prompts used for the experiment. I completed 20 ratings
before inspecting model annotation labels. ChatGPT subsequently saw ratings
in notebook tables. ChatGPT therefore had access to my ratings during development. However, my
ratings and evidence were excluded from every experimental annotation prompt.

## 2. Loading files and preparing Colab
I asked where to put the Numbers-exported CSV and how to activate a GPU.
ChatGPT guided uploading items.csv and items_rated.csv, loading them with pandas,
checking shape (20,5), column names, and using a Tesla T4. Later, after a new session,
the old notebook failed with FileNotFoundError for items.csv. The replacement embeds
the original tables and recreates the CSVs. Multiple active sessions caused a Colab
connection error; screenshots were used to distinguish the old and replacement notebooks
and terminate the old session. I later purchased Colab compute units myself, as recorded in section 10.

## 3. Descriptive results for my ratings
I requested code and text under the ratings plots. ChatGPT helped
produce the histogram, boxplot and counts, and drafted: 'The most frequent rating
was 3 (7 of 20 items). Overall, 13 items (65%) were rated in the toxic range (3–5),
while 7 (35%) were rated in the civil range (1–2). The median rating was 3, and the
middle 50% of ratings ranged from 2 to 4. These results describe the 20 sampled items.'
These quantities were checked against my unchanged ratings table.

## 4. Initial model and discussion pilot
I shared a successful SynDisco import and T4 check, then loaded
unsloth/Qwen2.5-3B-Instruct-bnb-4bit with max_out_tokens=80 and repetition_penalty=1.1.
ChatGPT provided a participant pool (Maria_K, Giannis, Kimya, Tom_77, Sofia),
seed 3352609, three selected participants, and four replies per discussion.
Initial instructions requested short English replies, responding to the original
and previous comments without repeating them. The first pilot repeated variations
on whether calling the politician 'Chump' was harsh.

## 5. Prompt revision and early full batches
ChatGPT revised the discussion instructions to request a new reason, example,
question or counterargument. I ran another pilot and posted its full text.
Some responses exceeded the requested sentence count, repeated points or addressed
an actor by their own name. I then generated all 20 discussions and shared
JSON files. An initial 80-token batch had incomplete endings. A later 160-token batch
still contained repetition and editing artifacts ('Sentence omitted', 'Sentence
included'), and an exact repeated reply in item 19. These batches were not accepted
as satisfactory final contexts. My original ratings were not changed.

## 6. Code and source review
I asked ChatGPT to review everything and edit the notebook directly.
ChatGPT inspected the assignment PDF, supplied sampling script, lab materials,
SynDisco documentation and version 2.2.1 source. It identified out-of-order setup,
duplicate development cells and an unseeded NumPy turn manager despite Python's seed.
The repair uses explicit np.random.default_rng(SEED + item_id), stable participant
selection, full shared context and checkpoints. Sampling was independently reconstructed
from pool.csv: all 20 comments in order match seed 3352609. The format of my labels and evidence was checked without changing my judgements.

## 7. Replacement model proposal
ChatGPT prepared a Qwen2.5-7B-Instruct 4-bit pilot on items 1, 8 and 19, chosen
because earlier discussions showed quality problems there. It proposed short replies,
no invented facts, and different conversational angles in C only. Both prompt and
model changed, so no isolated causal claim about model size is justified. The new
7B run had not yet been observed when the full implementation was prepared.

## 8. Request for a complete implementation
I asked ChatGPT to prepare a complete implementation and send me the notebook.
ChatGPT prepared the code for sections A–G, including the modified
2x2x2 gender/politics/education grid and empty-persona baseline, identical D/E
annotation instructions, exact prompt recording, JSON/evidence validation, invalid
counts, all four required agreement comparisons, matched-subset comparisons,
constant-label checks, plots, and English methodology and limitations.

ChatGPT used programmatic tests with a separate synthetic backend to check
ID alignment, caching, prompt equivalence, invalid handling and arithmetic. Such
tests are not a real model experiment. The provided notebook contains no fabricated
7B annotations or results. Numerical interpretation is generated from the actual
run and appended to markdown cells during export. At that preparation stage, real GPU execution, all-context
semantic review and a valid student GitHub repository remained necessary before
calling the file a completed submission. Subsequent execution, review and the
repository link are documented in sections 11–14.

## 9. Experimental prompts and outputs
The exact C instructions, pool, per-actor angles and random seed are printed in the
notebook code. The D/E instructions, exact dictionaries and full system/user prompts
appear in the annotation section and complete annotation tables. Every raw model
annotation, including invalid output, is retained there. This provides the direct
experimental record in addition to the coding-assistance summaries above.

## Status at the preparation stage
At this point, I had not yet run the full 7B notebook or created the GitHub
repository. ChatGPT had tested the implementation, but had not run the GPU
experiment. Sections 10–15 record my subsequent Colab run, the results review
and the repository link. The two submission files are the executed notebook and
this Markdown record; the JSON, CSV and ZIP files are working backups.

## 10. Colab limits and wording revisions
I shared screenshots of Colab connection problems and a GPU usage-limit message. ChatGPT explained the difference between too many active sessions and exhausted GPU access. I reported purchasing compute units; ChatGPT provided instructions for connecting the replacement notebook and running all cells. At that stage, successful execution of the new full 7B notebook had not yet been verified in the shared outputs. The subsequently completed run and its review are recorded in sections 11–13.

I asked for the report to use first-person wording such as “my ratings” and to explain my contribution more clearly. ChatGPT revised the prose without changing my original ratings or the experimental prompts. It explained that section G.3 requires an AI-use statement and a separate interaction record. I then said I had deleted the Colab contents and requested a complete fresh notebook. ChatGPT prepared a fresh copy, cleared prior execution outputs, and checked the code using a separate synthetic backend. These checks are software tests, not experimental results. I completed the initial ratings independently and ran the notebook in Colab, while ChatGPT helped with the implementation, debugging, organisation of the analysis and wording.

## 11. Completed 7B run and post-run audit (3 November 2026)
I ran the full notebook in Colab and supplied its checkpoint ZIP, then downloaded
and shared the executed notebook. The saved run contains 20 discussions and 360
annotation responses, with discussion configuration `d458ea986495f65c` and
annotation configuration `4368ba46ea43fd10`. ChatGPT checked the raw JSON, original texts, valid flags,
D/E prompt equivalence and agreement calculations. There are 280 complete responses
that meet the strict rule and 80 evidence failures; all 360 ratings are parsable.
The 80 failures comprise 44 extra-quotation-mark cases, 27 case-only mismatches
and 9 civil ratings with evidence instead of `not needed` (item 12, condition D).
The first two categories account for the 71 near-exact quotations rejected by the
strict evidence check. They remain invalid in the primary analysis.
The initial ratings, generated discussions and model annotation responses were not
changed during this review.

## 12. Comparing the Claude review with the actual outputs
I pasted a Claude review and asked ChatGPT what it thought. The initial review
reported every persona at 33.3% exact agreement, described the discussions as free
of repetition and concluded that context made the model stricter. ChatGPT checked
the saved responses and corrected the full ranges to 26.7–43.8% for exact ratings
and 73.3–86.7% for labels. The strict matched sample has 109 pairs, with six
civil-to-toxic changes and none in reverse; all 180 parsable-rating pairs have
11 civil-to-toxic and 17 toxic-to-civil changes. Thus the apparent direction depends
on evidence filtering. The strict primary results were retained, with a separately
labelled rating-only sensitivity check. No invalid evidence was repaired.

I then pasted Claude's acknowledgement and revised analysis. A further check found
that “19/20 without repetition” was still unsupported: item 5 contains a copied
sentence and other discussions repeat ideas. Whole-reply similarity for the copied
sentence plus an added sentence is about 0.837, below the screener's 0.90 threshold.
The four incomplete-ending flags are complete replies followed by emoji. Claims
about a psychological mechanism for “left” personas were not treated as findings.
This summary of the Claude review is based on the exchanges I pasted into
ChatGPT, rather than a complete export of my separate Claude conversation.

## 13. Editing the executed notebook
I asked how to download and send the notebook, followed the Colab File → Download
.ipynb steps, and supplied assignment_full(2).ipynb. ChatGPT revised the English
interpretation, clarified non-consecutive speaker returns and the education-grid
rationale, and restored missing original-data tables and rating plots by executing
only the deterministic A–B calculations in a separate CPU environment. Additional
invalid-response and rating-only sensitivity tables were calculated from the saved
JSON responses, without rerunning the language model. The original model outputs
and primary agreement outputs were preserved. The numerical review and wording
assistance are disclosed in the notebook. At that stage, the GitHub URL was still absent from the provided notebook.

## 14. Adding the repository link
I created the private GitHub repository `practical-data-science-assignment-1`
under `katerinaarmata-art` and shared its screenshot and URL:
https://github.com/katerinaarmata-art/practical-data-science-assignment-1
ChatGPT added that URL to the notebook title and configuration, updated the export
instructions and this log, and reran the final structural checks from the saved
responses. The model was not rerun.

## 15. Final consistency check and filenames (3 November 2026)
I shared a further review pointing out a mismatch between an older interaction
record and the notebook's disclosure of Claude assistance. I asked ChatGPT to
apply the corrections and label the files “the final”. The latest working record
already included the completed run and Claude review; ChatGPT made the historical
status statements explicit, added the configuration IDs and invalid-response
breakdown, and synchronized this file with the copy embedded in the notebook.

ChatGPT also executed only the configuration, imports and frozen-input cells
(zero-based cell indices 2, 4 and 5) in a separate local Python session to restore
their missing execution information and the two input-shape prints. This was not
a new Colab run. The notebook metadata identifies that local session. The 20
discussions, 360 annotation responses, original ratings and primary analysis
outputs were preserved; no model calls were made during this final edit. The
optional export cell remained unexecuted.

The final filenames are `the_final.ipynb` and `the_final_llm_interactions.md`.
The accompanying `the_final.zip` is only a convenient download of those two files.
I cannot confirm from the screenshots alone whether the kernel kept running
through the connection loss or whether any earlier reconnection repeated model
calls.

Finally, I asked ChatGPT to check that the report was written from my perspective.
It changed the remaining third-person descriptions, such as “the student asked”,
to first person and revised the notebook's introductory and submission notes.
The account of the assistance remained accurate, and no experimental data,
numerical results or saved outputs were changed during this wording edit.

After another review, I asked ChatGPT to help make the opening of G.2 easier to
read. I supplied my own reaction: the disagreement initially made me question my
ratings, while the similarity between the annotators made me think about polyphony
and checks and balances. ChatGPT drafted and revised a plain-English summary that
combined this reflection with the existing results, and I asked it to insert
“The story in short” at the start of G.2. This summary was written with AI
assistance, including help with wording, structure and the numerical explanation.

ChatGPT also checked the pasted review against the assignment and the existing
notebook. Unsupported grade predictions and absolute claims that identity had no
effect were not added to the results. The detailed comparisons and limitations
were retained. This edit changed explanatory text and synchronized the embedded
interaction record; it did not execute notebook cells, make model calls or change
ratings, generated responses, validity flags, calculations or saved outputs.

## 16. Final editing and submission checks
I asked ChatGPT to apply the remaining improvements within the available time.
It shortened repeated explanations, retained my reflection about disagreement,
polyphony and checks and balances, and organised G.2 around the four required
comparisons. It clarified the distinction between exact 1–5 agreement and
civil/toxic agreement, kept the numerical findings and limitations, and described
further prompt experiments as future work rather than completed work.

This was an editorial revision. The experiment code, original ratings, prompts,
generated discussions, annotations, saved outputs and execution counts were
preserved. The interaction record embedded in the optional export cell was updated
to match this file. No GPU run or new model call was made for this revision.
ChatGPT checked the final files for structural validity, consistency and preservation
of the saved results. This check did not constitute a new top-to-bottom Colab run.

I also asked for my reflection on polyphony and checks and balances to include
economics, politics, applied science and medicine, where decisions can have real
consequences. ChatGPT helped express this in simple English and distinguished my
broader reflection from the experiment's findings: high agreement is not proof
of bias or correctness, and different personas of the same model are not independent
reviewers. The medical example is illustrative, not an experiment or clinical claim.

Before submission, I asked to replace the broader application paragraph with two
specific sentences about agreement and checks and balances, removing the medical
example. ChatGPT inserted my supplied replacement without changing the results.
