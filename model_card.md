# 🎧 Model Card: VibeFinder 1.0

## 1. Model Name  
VibeFinder 1.0

---

## 2. Intended Use  
VibeFinder is designed to evaluate a user's target music preferences (Genre, Mood, Energy) and suggest songs from a curated catalog that match their desired vibe. 
It is intended for classroom exploration and simulation of content-based recommender algorithms. It should not be used in a production environment as a commercial product due to the extremely limited dataset catalog.

---

## 3. How the Model Works  
The model calculates a "Total Score" for every song based on three main rules:
- **Genre Match:** It awards 1.0 point if the song's genre perfectly matches the user's genre preference.
- **Mood Match:** It awards 1.0 point if the song's mood perfectly matches.
- **Energy Similarity:** It dynamically awards up to 2.0 points depending on how close the song's mathematical energy level is to the user's target energy level. 
The songs are then sorted from highest to lowest score to generate the recommendations.

---

## 4. Data  
The system uses the `data/songs.csv` catalog, which currently contains exactly 17 songs. Information about the songs includes subjective categorical points (like mood and genre) and Spotify audio feature metadata (like tempo, acousticness, and energy). 
The dataset features extreme limitations in niche diversity, featuring only 1 Rock song and 1 EDM song.

---

## 5. Strengths  
The system works exceptionally well for mainstream taste profiles (like "Happy Pop") because the dataset heavily caters to those specific genres. Furthermore, its simplistic categorical matching makes its recommendations extremely easy to logically explain to users visually. 

---

## 6. Limitations and Bias 
- This system heavily over-prioritizes the initial categorical matching, meaning completely mismatched vibe songs can sometimes outrank a perfect vibe match simply because they lie within the correct umbrella genre.
- When the user requests a niche profile (like Rock or EDM), the sheer scarcity of choices forces the system to recommend unrelated pop or lofi songs that simply share adjacent mood or energy levels. Thus, the system struggles to properly represent niche styles.
- The system doesn't account for acousticness or tempo, ignoring massive auditory differences.

---

## 7. Evaluation  
I tested the system against four distinct user profiles: "High-Energy Pop", "Chill Lofi", "Deep Intense Rock", and an edge-case adversarial profile "Edge Case Sad EDM".
I looked for how well the highest recommended songs aligned with both categorical constraints (genre/mood) and dynamic traits (energy).

I was surprised to find that the "Gym Hero" pop song consistently showed up across completely unrelated profiles (like Rock and Sad EDM) simply because its high energy stat mathematically overpowered other available tracks that had low energy, breaking the intended genre-filters due to the tiny volume of our catalog.  

---

## 8. Future Work  
If I kept developing this:
1. I would expand the `songs.csv` dataset drastically to ensure there are at least 5 baseline tracks for every mainstream genre.
2. I would add secondary logic checks preventing recommendations from drastically conflicting genres.
3. I would incorporate Danceability and Tempo mathematical matching loops to generate much tighter "Vibe" matches out of similar-scoring songs.

---

## 9. Personal Reflection  
### Biggest Learning Moment
My biggest learning moment was discovering how mathematically sensitive scoring algorithms are; halving the Genre weight completely destroyed the recommendation structure because high-energy pop songs suddenly mathematically overtook rock songs with mediocre energies!

### AI Tools Usage
Using AI tools dramatically sped up the actual formatting and documentation of the code. I had to double-check their outputs when the AI suggested using complex mathematical paradigms that were overkill for the simple matching logic we needed.

### Surprises about Algorithms
It was incredibly surprising how "human" the recommendations felt even though it was simply adding up categorical zeroes and ones and checking a decimal value distance. 

### Next Steps 
If I extended this project, I would dynamically fetch live song traits from the Spotify API to have a bottomless repository of data to test my mathematics on!
