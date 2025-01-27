# Activation Steering for LLMs

This repository contains an implementation of the contrastive activation steering method proposed in [Representation Engineering: A Top-Down Approach to AI Transparency](https://arxiv.org/abs/2310.01405) and [Activation Addition: Steering Language Models Without Optimization](https://arxiv.org/abs/2308.10248) which allows optimization free control over LLMs.

Similar to the famous word2vec kings-queens example, activation steerings finds that there are directions in the token representation space of LLMs that correspond to concepts. 

In practice, this means that we can find directions that correspond to the concept sentiment. By shifting their token representations along such a direction ("steering"), we can induce a significant change in the tone of the generation.


### Example

| Mode | Generation |
| --- | --- |
| Default | That game *was a real nail-biter! I'm glad we were able to come out on top in the end.* |
| +Happines | That game *was a real blast! I'm so glad we could celebrate together. I'm already looking forward to the next one!* |
| -Happines | That game *was a real heartbreaker. I'm still trying to process how we lost. I mean, we had them right where we wanted them, and then we just fell apart.* |

"That game" was given to Llama 3 8B as a context, while the remaining *tokens* were generated by the model. The mood of the generated text is altered by activation steering while keeping coherence. 

### Sentiment Analysis

We validate the effect by generating text from 580 beginnings of sentences with and without steering. The mood of the generated text is judged by a sentiment classification model. For Llama 3 8B, this yields the following average class probabilities:

| ![](Meta-Llama-3-8B-Instruct.png)|
|:--:|
| Change in average sentiment when applying activation steering to Llama 3 8B Instruct. |

We can deduce that activation steering allows controlling LLMs, at least the sentiment of the generated text. Note that this does not mean that the capabilities of LLMs remain the same regardless of whether steering is applied or not.

## References

The "all_truncated_outputs.json" dataset is from the RepE paper. [This model](https://huggingface.co/cardiffnlp/twitter-roberta-base-sentiment-latest) is used for the sentiment analysis.