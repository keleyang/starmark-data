# recommend.json Format Guide

## Structure Overview

```json
{
  "collections": [...],
  "creators": [...],
  "layout": [...]
}
```

---

## collections (Big Card - Collection)

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| id | String | Yes | Unique ID, e.g. "col1", "col2" |
| coverImageURL | String | Yes | Cover image URL, stored in `images/covers/` |
| title | String | Yes | Collection title |
| subtitle | String | No | Tag text above title, e.g. "Editorial Pick", "Trending" |
| editorial | String | No | Introduction paragraph shown in detail page |
| creators | [Creator] | Yes | Array of creators in this collection |

## creators (Small Card - Single Creator)

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| id | String | Yes | Unique ID, e.g. "1", "2" |
| name | String | Yes | Creator name |
| avatarURL | String | No | Avatar image URL, stored in `images/avatars/` |
| title | String | Yes | One-line title/tagline |
| bio | String | Yes | Detailed introduction |
| links | [Link] | Yes | Social media links array |
| previewImageURLs | [String] | No | Preview images array (reserved) |

### Link Object

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| platform | String | Yes | One of: `twitter`, `youtube`, `instagram`, `facebook` |
| url | String | Yes | Full profile URL |

## layout (Feed Order)

Controls the order of cards on the Recommend page.

| Field | Type | Description |
|-------|------|-------------|
| type | String | `"collection"` for big card, `"creator"` for small card |
| refID | String | Matches `id` in collections or creators |

---

## Image Naming

### Covers (`images/covers/`)
Format: `{collection_id}_cover.jpg`
- col1_cover.jpg
- col2_cover.jpg

### Avatars (`images/avatars/`)
Format: `{name_in_snake_case}.jpg`
- steve_krug.jpg
- marques_brownlee.jpg

---

## Full Example

```json
{
  "collections": [
    {
      "id": "col1",
      "coverImageURL": "https://raw.githubusercontent.com/keleyang/starmark-data/main/images/covers/col1_cover.jpg",
      "title": "Must-Follow UX & Product Design Creators",
      "subtitle": "Editorial Pick",
      "editorial": "Introduction text here...",
      "creators": [
        {
          "id": "1",
          "name": "Steve Krug",
          "avatarURL": "https://raw.githubusercontent.com/keleyang/starmark-data/main/images/avatars/steve_krug.jpg",
          "title": "Usability Expert",
          "bio": "Detailed bio here...",
          "links": [
            {"platform": "twitter", "url": "https://x.com/skrug"}
          ],
          "previewImageURLs": []
        }
      ]
    }
  ],
  "creators": [
    {
      "id": "1",
      "name": "Steve Krug",
      "avatarURL": "https://raw.githubusercontent.com/keleyang/starmark-data/main/images/avatars/steve_krug.jpg",
      "title": "Usability Expert",
      "bio": "Detailed bio here...",
      "links": [
        {"platform": "twitter", "url": "https://x.com/skrug"}
      ],
      "previewImageURLs": []
    }
  ],
  "layout": [
    {"type": "collection", "refID": "col1"},
    {"type": "creator", "refID": "1"}
  ]
}
```

## Notes

- Creators in `collections[].creators` are embedded with full data
- Creators in top-level `creators` are for small card display only
- `layout` determines the feed order; items not in layout won't show
- Image URL base: `https://raw.githubusercontent.com/keleyang/starmark-data/main/`
