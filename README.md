# Git Workshop Notes

Handout notes for attendees during my workshops on Git.

## Background

This book was originally a simple text file I wrote for myself when hosting sessions. I kept adding bits and pieces until it grew larger than what I'd personally call "speaker notes". I decided I should share these notes with the attendees. Using pandoc, I generated a pdf and shared it.

The book still remained closed source though. Very recently, I realised that a book about Git that I wrote, being closed source doesn't make sense. So I rearranged it, and published to GitHub under the MIT license. The repo contains everything you need to generate a pdf on your system.

## Building this book

Install `pandoc`. Then run

```
make pdf
```

to generate pdf at `build/pdf/book.pdf`.

## License

The source code of this book is distributed under [MIT License](./LICENSE.md). However, the resulting PDF is distributed under Creative Commons Attribution-ShareAlike 4.0 International. To view a copy CC-BY-SA 4.0, visit [http://creativecommons.org/licenses/by-sa/4.0/](http://creativecommons.org/licenses/by-sa/4.0/)
