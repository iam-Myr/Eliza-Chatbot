# Sentence Generation

## Dataset Choice

The selection process for the ten books aimed to exclude poetic, biblical, or otherwise abnormal texts, such as those containing numbered verses. A diverse range of authors was chosen to ensure variations in vocabulary and speech patterns. The size of the vocabulary was 37,997 unique words.

## Data Structure

The data structure chosen to hold the n-grams is a tree, specifically a trie. A trie stores keys by breaking them down into their constituent words or elements, with each node in the trie representing a single word of the key.

### Advantages of a Trie

- **Efficient Storage**: A tree structure allows for efficient storage of all n-grams simultaneously, eliminating the need to create separate structures for each n-gram length.
- **Faster Sentence Generation**: Once the trie is built, sentence generation operations become significantly faster compared to frequency dictionaries.

## Sentence Generation Process

### Starting n-gram

The sentence generation process begins with a starting n-gram. The program uses the `generate_next_word` function iteratively until the desired sentence length is achieved. If no suitable words are found, a word is randomly selected from the vocabulary.

### Generate Next Word Function

The `generate_next_word` function operates on a sentence of length n-1, corresponding to the n-grams used for generating sentences. The function traverses the tree structure recursively, selecting the next word based on frequency.

- **Base Case**: When the sentence length is zero, it randomly selects a word if the current word has children; otherwise, it returns `None`.
- **General Case**: The function checks if the current word has the next word as a child. If it does, the function proceeds; otherwise, it returns `None`.

### Sentence Generation Examples

#### 2-grams
1. The only way to move him was to depend.
2. His situation is an evil but you must give me a living.

#### 3-grams
1. Churchill after being disliked at least years was now spoken of with compassionate allowances.
2. Repeated the doctor with a start but what on earth can he agent he thought mahanaim where he adam at the news with chilling gripe of sorrow stood that.

#### 4-grams
1. Who will none shall from me withhold thy offered good distance from those she wants to be with but one cannot comprehend a young being under such restraint.
2. Doated introductions Jonah and the whale.

#### 5-grams
1. Alice had been looking over his shoulder with some curiosity.
2. Had he anything to tell the prince.

#### 6-grams
1. Grant when he heard of all this endeavored to discover what could have offended his neighbor but all explanation was prevented by the obstinate silence of Oakley.
2. So almost every hour when the watches of the night were set and the band on deck sentinelled the slumbers of the band below and when if a rope.

## Smoothing

The model incorporates smoothing similar to Laplace smoothing. It builds a vocabulary of unique words and assigns them a frequency of 1 or less. A parameter called "creativity" controls the frequency of smoothed words.

## Thoughts

Sentence generation is a fascinating area of study, though challenging because even a single misplaced word can disrupt the coherence of the entire sentence. Experimenting with larger datasets or different smoothing techniques could yield interesting results.

## Bonus: Text-to-Image Prompts

The sentence generation technique could be used to create prompts for text-to-image models. An example sentence generated from a story:

- **Story**: "The knight stands opposite of the Dragon..."
- **Generated Sentence**: "A pointy spear points at the beast's direction."

## Conclusion

This project demonstrates a unique approach to sentence generation using n-grams and trie data structures, offering a foundation for further exploration in natural language processing.

