---
layout: post
title: 추천 시스템 레퍼런스 - 스포티파이
date: 2025-08-16 14:45 +0900
categories: [Data Science, References]
tags: [datascience, ds, reference]
description: DS 추천시스템 프로젝트 레퍼런스
---


# Recommendation System

- Spotify’s personalized playlists minimize listeners’ selection cognitive load

## Hybrid Filtering

- Collaborative Filtering (shared models): creating a map of music based on user behaviours and patterns.
	- playlist에 같은 곡이 있는 사람들끼리 cluster를 이룸
	- user behaviours, preferences, playlist creation, track listening history, metadata 등 이용
	- 사용자들이 특정 곡들을 함께 자주 재생 목록에 추가할 경우, 이 곡들은 지도 상에서 서로 가까이 배치되어 유사성을 강조

  - Content Based Filtering: metadata, raw audio analysis 고려.
	  - metadata: release date, label, artist, album, genre, duration, key signature, mode(major/minor), rhythmic structure, tempo, explicit/sensitive content, language, instruments, featured artists, collaborators, producer, lyrics, cover art, music video, cultural context, geographical origin
		  - cultural context: How the track is discussed in articles, blogs, and media, capturing its broader significance. 
	  - raw audio analysis: Danceability, Loudness, Loudness variance, Energy, Valence, Tempo, Acousticness, Instrumentalness, Speechiness, Key, Mode, rhythmic structure, duration, Beat and bar strength, chord progressions, melody characteristics
  
- 특히 ML + NLP는 track의 오디오적 특징과 각 노래를 특별하게 만드는 contextual element를 capture 하게 해줌
- $\rightarrow$ 노래를 '분위기' 같은 거로 categorize 할 수 있게 됨
## 유저의 반응

- "What's New" tab, the primary goal of the listening session is often to quickly explore music recently added to the platform. In that context, high skip rates are to be expected, as the user's primary goal is to skim through the feed and save some of the content served for later — which means that a track skip shouldn't be interpreted as a definite negative signal. On the other hand, if the user skips a track when listening to a "Deep Focus" playlist designed to be consumed in the background, that skip is a much stronger sign of user dissatisfaction.

- **Explicit, or active feedback:** library saves, playlist adds, shares, skips, click-through to artist/album page, artist follows, "downstream" plays 
- **Implicit, or passive feedback:** listening sessions length, track playthrough, and repeat listens
  

## 추후 적용방법

  
  

# References

- https://medium.com/beyond-the-build/the-inner-workings-of-spotifys-ai-powered-music-recommendations-how-spotify-shapes-your-playlist-a10a9148ee8d
- 
