## set a maximum number of lines of text with CSS / line-clamp

```
.card__preview-text {
  --max-lines: 3;

  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-line-clamp: var(--max-lines);
  overflow: hidden;
}
```
