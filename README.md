<H1 ALIGN =CENTER>Ex-7 Implementation of Text Summarization</H1>
<H3>Name: Krithick Vivekananda </H3>
<H3>Register No: 212223240075</H3>
<H3>Date: </H3>


## Aim:
To perform Automatic Text Summarization using Natural Language Processing (NLP) techniques
 
## Algorithm:
<b>Step 1:</b> Import necessary libraries for natural language processing tasks

<b>Step 2:</b> Download NLTK resources, including the punkt tokenizer and stopwords

<b>Step 3:</b> Define Text Preprocessing Function to tokenize, remove stopwords, and perform stemming

<b>Step 4:</b> Define the Text Summarization Function using a simple frequency-based approach<br>
    - Calculate the frequency of each word in the preprocessed text<br>
    - Calculate a score for each sentence based on the sum of word frequencies<br>
    - Select the top N sentences with the highest scores to form the summary<br>
    
<b>Step 5:</b> Construct the main program to read the paragraph  and perform text summarization<br>
      - Generate and print the original text<br>
      - Generate and print the text summary using the Text Summarization function<br>
      
## Program:
```python
import nltk
from nltk.corpus import stopwords
from nltk.tokenize import word_tokenize, sent_tokenize
from nltk.stem import PorterStemmer

# Download required packages
nltk.download('punkt_tab')
nltk.download('stopwords')

def preprocess_text(text):
    # Tokenize text into words
    words = word_tokenize(text)

    # Remove stopwords and punctuation
    stop_words = set(stopwords.words('english'))

    filtered_words = [
        word for word in words
        if word.lower() not in stop_words and word.isalnum()
    ]

    # Stemming
    stemmer = PorterStemmer()

    stemmed_words = [
        stemmer.stem(word)
        for word in filtered_words
    ]

    return stemmed_words

def generate_summary(text, num_sentences=3):
    # Tokenize into sentences and remove extra spaces/newlines
    sentences = [
        sentence.strip()
        for sentence in sent_tokenize(text)
    ]

    # Preprocess text
    preprocessed_text = preprocess_text(text)

    # Calculate word frequencies
    word_frequencies = nltk.FreqDist(preprocessed_text)

    # Dictionary for sentence scores
    sentence_scores = {}

    # Score each sentence
    for sentence in sentences:

        for word, freq in word_frequencies.items():

            if word in sentence.lower():

                if sentence not in sentence_scores:
                    sentence_scores[sentence] = freq

                else:
                    sentence_scores[sentence] += freq

    # Select top N sentences
    summary_sentences = sorted(
        sentence_scores,
        key=sentence_scores.get,
        reverse=True
    )[:num_sentences]

    # Join summary sentences properly aligned
    return '\n    '.join(summary_sentences)


if __name__ == "__main__":
    input_text = """
    The piano sat silently in the corner of the room.
    Nobody could remember the last time it had been played.
    The little girl walked up to it and hit a few of the keys.
    The sound of the piano rang throughout the house for the first time in years.
    In the upstairs room, confined to her bed, the owner of the house had tears in her eyes.
    """

    # Generate summary
    summary = generate_summary(input_text)

    # Print original text
    print("\nOriginal Text:")
    print(input_text)

    # Print summary
    print("\nSummary:\n")
    print("    " + summary + '\n')
```

## Output:
<img width="835" height="297" alt="image" src="https://github.com/user-attachments/assets/8b3d0393-b947-496a-a025-05cfbdfd720b" />

## Result:
Thus, the program to perform Text Summarization is executed sucessfully
