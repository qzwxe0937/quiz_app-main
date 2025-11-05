# Quiz App Selection Algorithm

This document summarizes how questions are chosen during practice. The logic is kept
outside the code so that the behaviour remains clear even if the implementation
changes.

## Two‑phase selection

1. **Pick a category**
   - While any unseen questions remain, 70% of selections are drawn from that pool,
     20% from previously wrong questions and 10% from fully correct ones.
   - When the unseen pool is empty, its share becomes zero and the remaining
     categories receive 70% (wrong) and 30% (correct).
   - If a category has no questions, its portion is redistributed to the other
     available categories in the original 7/2/1 ratio so that the total remains 100%.
2. **Pick a question within the category**
   - Unseen questions are chosen uniformly so every new item appears with the same
     chance.
   - Previously wrong questions are weighted by `wrong rate + 0.05`. Items answered
     incorrectly more often surface more frequently.
   - Fully correct questions use `1 - correct rate + 0.05` so well mastered items
     appear only occasionally but are never completely ignored.

This approach ensures new material is prioritised but also reinforces weak spots
and retains some long‑term revision.
