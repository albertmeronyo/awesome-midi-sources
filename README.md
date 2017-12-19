# MIDI-sources

A list of sites with MIDI files on the Web.

- http://midi-files-for-free.biz/ Large collection of pop-rock MIDI files
- http://www.midiworld.com/ Likewise. Downloadable by appending /download/ID
- https://freemidi.org Likewise
- http://www.jsbach.net/midi/ Works by J.S. Bach
- http://www.vgmusic.com/ MIDI files from videogames
- https://www.reddit.com/r/WeAreTheMusicMakers/comments/3ajwe4/the_largest_midi_collection_on_the_internet/ The largest MIDI collection on the Internet
- https://www.reddit.com/r/SongStems/comments/1vqwj2/i_got_more_stems_than_ive_got_gray_hairs_and/ Song stems
- https://www.reddit.com/r/SongStems/comments/17eiwr/hey_guys_i_finally_got_my_16ish_gig_stem/ Song stems
- https://www.reddit.com/r/WeAreTheMusicMakers/comments/3anwu8/the_drum_percussion_midi_archive_800k/ Drump percussion MIDI archive
- http://scummbar.com/ Monkey Island MIDIs (these deserve their own entry)
- Find a way to export all Guitar Pro files in MySongBook to MIDI <-- nicely sorted collection
- https://www.reddit.com/r/WeAreTheMusicMakers/comments/3anwu8/the_drum_percussion_midi_archive_800k/ Drum percussion MIDI archive

- MuseData: http://musedata.org/ Library of classical music scores (MIDI, MuseData, Humdrum)
- The Josquin Research Project: http://josquin.stanford.edu/ Complete score of polyphonic music from ~1420-1520 (MIDI, Humdrum, MuseData, MusicXML, MEI, ...)
- The MIDI Archive: http://archive.cs.uu.nl/pub/MIDI/ MIDI and other electronic music stuff (with link to other MIDI sites) 
- J. S. Bach MIDI Page: http://bachcentral.com/ Dedicated to J. S. Bach (MIDI) 

## MIDI-LD stats

On the reddit dump ([full list](midi_list.txt))
- 119,502 MIDI files
- 113,565 nquad files (95.03% over the total, 4.96% failure rate)
- 4,911,643,092 triples

## Wat te doen
- HAS TO BE MEANINGFUL FOR LINKED DATA PERSONS AND MUSIC PERSONS
- SEMANTIC WEB TASKS
  - Linking each named graph to the best matching URI in the LOD cloud -- DBpedia, wikidata, musicbrainz/linkedbrainz, etc
    - Using text: LOTUS
    - Using music: shazam/soundhound API
    - Using both? Other?
  - Audiolization: musical interface for finding / accessing data
- Musician / musicologist TASKS
  - The LD jukebox: Composing by mixing using SPARQL CONSTRUCT -- mashups!
  - Music annotation (i.e. mixing vocabularies)
  - ???
- Both: searching musical LD by means of musical similarity metrics -- Search the MIDI cloud using musical similarity metrics (a la LOTUS) and list the results

- Non-functional requirements: easy to implement, minimal UI


## Conclusions

1. The linking paper comes first (because the other papers need it!)
2. The IR / composer papers come next

How do we do the linking paper?
Option 1. Fingerprints with chromashit transforming the MIDI to MP3
Option 2. Match Incipits of https://opac.rism.info/metaopac/singleHit.do?methodToCall=showHit&curPos=1&identifier=251_SOLR_SERVER_1577181594
with Reinier-separated MIDI tracks

### Outline
- We have a random dump of MIDI files we want to link to Web resources
- We represent those MIDI as Linked Data
- We look for other Linked Data resources on the Web
- PROBLEM: MIDI-LD (database A) only contain (symbolic) musical information
- (Actually that's not true: they mostly contain *some* metadata in textual form, but we cannot assume it)
  - Actually: 109,725 out of 113,565 contain some label (96.62%)
- PROBLEM: those other Linked Data resources on the Web (database B) DO NOT contain any musical information
- PROBLEM (short): there's no overlap between musical info (in database A) and textual info (in database B)
- WE ARE ARGUING THAT LD DATABASES SHOULD CONTAIN JUST A LITTLE BIT OF SYMBOLIC MUSICAL INFORMATION (identifying the song)
- NO
- WE ARE ACTUALLY ARGUING IS THAT THERE MUST BE A THRESHOLD ON HOW MUCH TEXTUAL INFORMATION MUSICAL DATABASES MUST CONTAIN, AND HOW MUCH MUSICAL INFORMATION TEXTUAL MUST DATABASES CONTAIN
- (E.g. only textual information gets 40% of the songs correctly linked, you need symbolic music info to accurately link the rest)
- Except for: RISM, who have INCIPITS
- Incipits are the first 10 notes of the melody of a song
- We take the MUSEdata database musedata.org

## Linking overview

- Try to distinguish melody track, and then use shazam/soundhound (w/ Rob Macrae)
- Text from filename + metadata, and then link using NLP/LOTUS
- Machine Learning, crowdsourcing


- Enrich DBpedia with the symbolic notes
- Link lyrics to MIDIs
- Link to (from) Spotify tracks

## Linking to LOD using LOTUS

- Using file names : `find 130000_Pop_Rock_Classical_Videogame_EDM_MIDI_Archive\[6_19_15\] -type f -name "*.mid" -exec basename {} \;`
- Using MIDI textual metadata

## DATASET FILES

- Raw conversion of MIDI to RDF
- MIDI metadata (pitches, instruments, etc -> MIDI resources that don't belong to the vocab)
- Links: to lyrics
- Links: to LOTUS top matches
- Links: to DBpedia
- Links: to Spotify
- Links: from DBpedia to this MIDI track (incipits) --> find encoding in Literals like in RISM

## Related work

- GitHub plays when you commit http://thenextweb.com/apps/2016/10/03/this-site-tracks-events-across-github-to-generate-calming-work-music/



- Look into other kinds of MIDI events for text metadata
- HDT
- Use textual labels (trackname, meta, lyrics) as entry point for musical events
- Find unparsed [1,2,3] events
- Connect musical events to semantic concepts --> word2vec to assign music to unlabelled concepts
- Combination of text, symbolic matching, shazam
- Convert it into a challenge / marchine learning contest, give evaluation / gold standard (public + private evaluation sets)
- Use http://labrosa.ee.columbia.edu/millionsong/pages/example-track-description and compare key of the algorithm + key we infer from MIDI with state-of-the-art algorithm
- Use http://mirg.city.ac.uk/codeapps/the-magnatagatune-dataset


- Open GitHub organization "The MIDI Society" <- come up with catchy name
  - MIDIpedia
  - Others?

## After VU meeting TODO

More datasets:
- Mysongbook to MIDI and add to MIDI dump
- Find name of eHumanities presenters doing catchyness / motif identification

Text part:
- LOTUS part / retrieval indexing - infrastructure to query dataset
- Decide later on long tail / NED

Symbolic part:
- Compile RISM and make it queryable
- Prototype to match classical music MIDIs with incipits

ML challenge part:
- Baseline with song names: (midi_song_names x dbpedia+MB_song_names) <- find best matches here (link prediction / entity resolution task)
- "Identity problem": linking musical pieces to particular subsets of suites / the whole suite?
