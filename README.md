# Korean Holidays

Korean public holidays data with automatic daily updates from [data.go.kr](https://www.data.go.kr/data/15012690/openapi.do) (Korea Astronomy and Space Science Institute).

## Features

- Daily automatic updates via GitHub Actions
- Includes regular holidays, substitute holidays, and temporary holidays
- Free to use (MIT License)
- No rate limits (GitHub CDN)

## Usage

### Raw URL

```
https://raw.githubusercontent.com/raki-1203/korean-holidays/main/holidays/{year}.json
```

### Example (Swift)

```swift
let year = Calendar.current.component(.year, from: Date())
let url = URL(string: "https://raw.githubusercontent.com/raki-1203/korean-holidays/main/holidays/\(year).json")!

let (data, _) = try await URLSession.shared.data(from: url)
let holidays = try JSONDecoder().decode([Holiday].self, from: data)

struct Holiday: Codable {
    let dateKind: String
    let dateName: String
    let isHoliday: String
    let locdate: Int
    let seq: Int
}
```

### Example (JavaScript)

```javascript
const year = new Date().getFullYear();
const response = await fetch(`https://raw.githubusercontent.com/raki-1203/korean-holidays/main/holidays/${year}.json`);
const holidays = await response.json();
```

## JSON Schema

```json
[
  {
    "dateKind": "01",
    "dateName": "Holiday Name",
    "isHoliday": "Y",
    "locdate": 20260101,
    "seq": 1
  }
]
```

| Field | Description |
|-------|-------------|
| `dateKind` | Type code ("01" = national holiday) |
| `dateName` | Holiday name in Korean |
| `isHoliday` | "Y" = public holiday |
| `locdate` | Date in YYYYMMDD format |
| `seq` | Sequence number |

## Data Source

- **Provider**: Korea Astronomy and Space Science Institute (KASI)
- **API**: [data.go.kr Special Days Information Service](https://www.data.go.kr/data/15012690/openapi.do)
- **Update Frequency**: Daily at 00:00 UTC (09:00 KST)

## Setup (for contributors)

1. Get API key from [data.go.kr](https://www.data.go.kr/)
2. Add `DATA_GO_KR_API_KEY` to repository secrets
3. GitHub Actions will automatically update holidays daily

## License

MIT License - Free to use for any purpose.

## Related Projects

- [my-calendar-app](https://github.com/raki-1203/my-calendar-app) - iOS calendar app using this data
