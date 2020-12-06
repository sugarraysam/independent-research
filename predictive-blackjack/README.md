# Predictive Blackjack

## Hypothesis

Given sufficient past information about the last output from a Random Number Generator (RNG), a properly trained reinforcement learning agent can predict the future output of the given RNG with better accuracy then a random agent.

**Sub-hypothesis**

The random agent will find that the probability of the next card's value being 10 is higher than other probabilities and should be biased towards predicting 10 as the next output.

## Environment

We will base our research on a problem derived from Blackjack. Our RNG will sample the next card's value according to a valid 6-deck probability distribution. The output is between 1 and 10. We do not care about the kind of the card (Heart, Spade, Diamond or Club) and are only focused on the value, as this is what matters to a blackjack agent.

**Reward**

- -1 for bad prediction
- +1 for accurate prediction

**State**

- Probability distribution of the next card's value
- 10 floats between 0 and 1, that sum to 1 where `p(i) = N(i) / N(total)`, and `sum(p(i)) == 1.0`
- Initial values are, for all `i`, `N(i) = 1`, `N(total) = 10` and `p(i) = 0.1`
- State is adjusted after each and every draw

**Action**

- Output a probability distribution over the next card's value
- 10 outputs, with a softmax layer, where `p(j) in [0,1]` and `sum(p(j)) = 1.0`
