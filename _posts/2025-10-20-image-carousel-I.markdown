---
layout: post
title: "Build a Image Carousel component in React"
date: 2025-10-20 19:50:00 +0800
categories: javascript, typescript, coding
math: true
---

# Question

Build an image carousel that displays a sequence of images.

## Requirements

The image carousel component takes in an array of image URLs. Example image URLs are provided in the skeleton code.

### Layout and positioning:

- The image carousel should be centered on the screen with a maximum size of 600px by 400px.
- Images should shrink to fit within the carousel so that the entire image is visible. Empty parts of the carousel can be filled with black.
- If the screen width is smaller than the image, the carousel should be resized to fit within the available horizontal space.

### Navigation:

- Add left/right navigation buttons to allow the user to navigate through the images. The buttons should allow a cycling behavior, i.e. after the last image, the image cycles back to the first.
- Add page buttons at the bottom to directly jump to an image. You may assume there will be fewer than 10 images.
- Animations and transitions are not necessary for this question, they will be explored in Image Carousel II and Image Carousel III.

## Solution:

```react
import { useState } from 'react';

import ImageCarousel from './ImageCarousel';

const images = [
  {
    src: 'https://picsum.photos/id/600/600/400',
    alt: 'Forest',
  },
  {
    src: 'https://picsum.photos/id/100/600/400',
    alt: 'Beach',
  },
  {
    src: 'https://picsum.photos/id/200/600/400',
    alt: 'Yak',
  },
  {
    src: 'https://picsum.photos/id/300/600/400',
    alt: 'Hay',
  },
  {
    src: 'https://picsum.photos/id/400/600/400',
    alt: 'Plants',
  },
  {
    src: 'https://picsum.photos/id/500/600/400',
    alt: 'Building',
  },
];

export default function App() {
  const [message, setMessage] = useState('Image Carousel');

  return (
    <div className="wrapper">
      <ImageCarousel images={images} />
    </div>
  );
}
```

```react
import { useState } from "react";

function clsx(...classnames: Array<any>) {
  return classnames.filter(Boolean).join(" ");
}

export default function ImageCarousel({
  images,
}: Readonly<{
  images: ReadonlyArray<{ src: string; alt: string }>;
}>) {
  const [currIndex, setCurrIndex] = useState(0);
  const currImage = images[currIndex];
  return (
    <div className="image-carousel">
      <img
        src={currImage.src}
        key={currImage.src}
        alt={currImage.alt}
        className="image-carousel__image"
      />
      <button
        aria-label="Previous Image"
        className="image-carousel__button image-carousel__button--prev"
        onClick={() => {
          const prevIndex = (currIndex - 1 + images.length) % images.length;
          setCurrIndex(prevIndex);
        }}
      >
        &#10094;
      </button>
      <button
        aria-label="Next Image"
        className="image-carousel__button image-carousel__button--next"
        onClick={() => {
          const prevIndex = (currIndex + 1) % images.length;
          setCurrIndex(prevIndex);
        }}
      >
        &#10095;
      </button>
      <div className="image-carousel__pages">
        {images.map(({ src, alt }, index) => (
          <button
            className={clsx(
              "image-carousel__pages__button",
              index === currIndex && "image-carousel__pages__button--active",
            )}
            aria-label={`Navigate to ${alt}`}
            key={src}
            onClick={() => {
              setCurrIndex(index);
            }}
          />
        ))}
      </div>
    </div>
  );
}
```

```css
* {
  box-sizing: border-box;
  margin: 0;
}

body {
  font-family: sans-serif;
}

.wrapper {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;

  height: 100vh;
  width: 100vw;
}

.image-carousel {
  background-color: rgba(0, 0, 0);
  height: 400px;
  width: min(600px, 100vw);
  overflow: hidden;
  position: relative;
}

.image-carousel__image {
  position: absolute;
  object-fit: contain;
  inset: 0;
  width: 100%;
  height: 100%;
}

.image-carousel__button {
  height: 40px;
  width: 40px;

  background-color: rgba(0, 0, 0, 0.5);
  color: white;
  border: none;
  border-radius: 100%;
  cursor: pointer;

  position: absolute;
  top: 50%;
  transform: translateY(-50%);
}

.image-carousel__button:hover {
  background-color: rgba(0, 0, 0, 1);
}

.image-carousel__button--prev {
  left: 16px;
}

.image-carousel__button--next {
  right: 16px;
}

.image-carousel__pages {
  background-color: rgba(0, 0, 0, 0.5);
  border-radius: 12px;
  display: inline-flex;
  gap: 8px;
  padding: 8px;

  position: absolute;
  bottom: 24px;
  left: 50%;
  transform: translateX(-50%);
}

.image-carousel__pages__button {
  height: 8px;
  width: 8px;

  border: none;
  border-radius: 100%;
  background-color: rgba(155, 155, 155);
  cursor: pointer;
  display: inline-block;
  padding: 0;
  transition: background-color 0.3s ease-in-out;
}

.image-carousel__pages__button:hover {
  background-color: rgba(255, 255, 255);
}

.image-carousel__pages__button--active {
  background-color: rgba(255, 255, 255);
}
```
