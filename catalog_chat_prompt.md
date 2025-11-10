# Pony Express Archive Indexing Task

You are indexing articles and photos from "The Pony Express," the North Mesquite High School newspaper from the 1974-1975 school year. Your goal is to create searchable catalog entries that help alumni and researchers discover content.

## Input Format
You will receive the text content from a single issue, organized by page number.

## Output Format
Generate a JSON array with one object per article or photo. Use this exact structure:

```json
{
  "IssueDate": "YYYY-MM-DD",
  "IssueFile": "YYYY-MM-DD.pdf",
  "Type": "Article" | "Photo",
  "Section": "string",
  "Title": "string",
  "Page": number,
  "Author": "string",
  "Names": ["array of strings"],
  "Topics": ["array of strings"],
  "Organizations": ["array of strings"],
  "Artists": ["array of strings"],
  "PublicFigures": ["array of strings"],
  "Events": ["array of strings"]
}
```

## Field Instructions

### Core Fields (ALWAYS REQUIRED)

**IssueDate**: The publication date in ISO format (YYYY-MM-DD). This will be provided.

**IssueFile**: The PDF filename (YYYY-MM-DD.pdf). This will be provided.

**Type**: 
- Use `"Article"` for written content with text/reporting
- Use `"Photo"` for standalone photos with captions, group photos, action shots

**Section**: 
- Use the section name as printed in the newspaper (e.g., "Sports", "Editorial", "Opinions", "News", "People", "Sharps and Flats")
- For subsections, use format: "Section - Subsection" (e.g., "Opinions - Inside Views")
- Common sections: Editorial, Opinions, News, People, Sports, Action, Sharps and Flats, Key Notes, Bits N Pieces, Hodge Podge, The Spirit People

**Title**: 
- Use the headline exactly as written
- For context, add clarifying details in parentheses: "Title (context)"
- Examples: 
  - "New music assistant (Mrs. Connie Hamrick)"
  - "Now comes Jerry (President Gerald Ford)"
  - "Varsity Cheerleaders (Group Photo)"
- For photo captions without clear titles, create descriptive title: "New Faculty Group Photo"

**Page**: The page number where the content appears (as an integer)

**Author**: 
- Use the byline name(s) exactly as printed
- If multiple authors, use format: "NAME1 and NAME2"
- **IMPORTANT: If no byline present, use empty string: `""`**
- **IMPORTANT: For photos, use empty string: `""` (only include photographer name if explicitly credited)**
- For editorials without bylines, use: `"Editorial Board"`

### Discovery Fields (ALWAYS INCLUDE - use empty arrays if none apply)

**Names** (HIGH PRIORITY):
- Include ALL people mentioned in the article or photo
- Include the author(s) in this array
- Use names exactly as written in the article (with titles/honorifics)
- For photos: include everyone identified in the caption
- Examples: `["GLENN HUGHES", "Gerald Ford", "Richard Nixon"]`
- Examples: `["Mrs. Shirley Goolsby", "Coach Brent Thorne", "Steve Dailey"]`
- For "Staff" or group listings: include individual names if provided

**Topics** (HIGH PRIORITY):
- Use 1-4 standardized topic tags from the controlled vocabulary
- Choose the most specific relevant tags
- For sports: always include both the sport (`"football"`) and `"sports"`
- For reviews: include both the type (`"album review"`) and general (`"music review"`)
- Examples: `["football", "sports"]`, `["band", "marching band"]`, `["politics", "editorial"]`

**Organizations** (HIGH PRIORITY):
- List all school clubs, teams, departments, or external organizations mentioned
- Use full, clear names: `"Varsity Football Team"` not just "Varsity"
- Include opponent schools for sports articles
- Examples: `["Varsity Band", "Stage Band"]`, `["French Club"]`, `["Bryan Adams High School"]`

**Artists** (MEDIUM PRIORITY - mainly for entertainment content):
- For music reviews: list musicians, bands, or composers mentioned
- For concert coverage: performing artists
- Use full names: `"Richard Betts"`, `"Allman Brothers Band"`
- Leave empty array if not applicable: `[]`

**PublicFigures** (LOWER PRIORITY - mainly for opinion/news pieces):
- Politicians, celebrities, or other public figures mentioned
- These are people NOT affiliated with the school
- Examples: `["Gerald Ford", "Richard Nixon", "Nelson Rockefeller"]`
- Examples: `["Elvis Presley", "Paul McCartney"]` (when mentioned as cultural references)
- Leave empty array if not applicable: `[]`

**Events** (LOWER PRIORITY - named specific events):
- Specifically named events with dates/times
- Examples: `["September 20-21 Debate Tournament"]`, `["Homecoming Dance"]`, `["UIL District Competition"]`
- Do NOT include: generic references like "football game" or "meeting"
- Leave empty array if not applicable: `[]`

## Controlled Vocabulary

### Topics - Use ONLY these standardized terms:

**Sports:** football, basketball, baseball, track, volleyball, tennis, golf, cross country, sports (general)

**Arts:** band, marching band, concert band, stage band, jazz, choir, acappella, vocal music, orchestra, drama, theater, play, musical, dance

**Spirit:** cheerleaders, cheerleading, majorettes, twirling, drill team, pep squad, pep rally, spirit week

**Clubs:** debate, speech, student council, journalism, newspaper, yearbook, national honor society, science club, math club, french club, spanish club, art club, vocational education, vica, oea, junior achievement

**Academic:** special education, plan a program, honors, advanced placement

**Entertainment:** music review, album review, concert review, movie review, film review, book review, concert, performance

**Events:** homecoming, prom, dance, graduation, senior events, awards, scholarship, recognition, assembly, fundraiser

**Editorial:** politics, political commentary, editorial, opinion, commentary, current events, news analysis, school policy

**Other:** new teachers, new students, faculty, profiles, interviews, features, campus improvements, facilities, schedule, calendar

## Quality Guidelines

1. **Be thorough with Names**: This is the most important field. Alumni searching for themselves or friends depend on this.

2. **Be consistent**: Use the same spelling/format throughout (e.g., always "Mrs. Shirley Goolsby", not sometimes "Shirley Goolsby")

3. **Preserve honorifics**: Keep "Mrs.", "Mr.", "Miss", "Coach", "Dr." as written

4. **Use standardized Topics**: Don't invent new topic terms - use only from the controlled vocabulary

5. **Be specific with Organizations**: "Varsity Football Team" is better than just "Football"

6. **Context in Titles**: Add parenthetical context to make titles searchable and clear

7. **Empty arrays/strings, not nulls**: Use `[]` for empty fields, never `null` or omit the field. Use `""` for empty Author field.

8. **Author field**: Leave blank (`""`) unless there is an explicit byline or photographer credit

## Example Entries

### Example 1: Sports Article
```json
{
  "IssueDate": "1974-09-11",
  "IssueFile": "1974-09-11.pdf",
  "Type": "Article",
  "Section": "Sports",
  "Title": "Stallions stop Cougars, take 19-9 victory",
  "Page": 16,
  "Author": "MARTY MCLENDON",
  "Names": ["MARTY MCLENDON", "Steve Dailey", "Gary Lacey", "Richard Brown", "Larry Jones", "Steve Ewton", "Don Wafford", "Terry Davis", "David Jennings", "Ted Small", "Mike West"],
  "Topics": ["football", "sports"],
  "Organizations": ["Varsity Football Team", "Bryan Adams High School"],
  "Artists": [],
  "PublicFigures": [],
  "Events": []
}
```

### Example 2: Music Review
```json
{
  "IssueDate": "1974-09-11",
  "IssueFile": "1974-09-11.pdf",
  "Type": "Article",
  "Section": "Sharps and Flats",
  "Title": "Richard Betts 'Highway Call' Album Review",
  "Page": 12,
  "Author": "RICHARD PRADARITS and PAUL NEELEY",
  "Names": ["RICHARD PRADARITS", "PAUL NEELEY", "Richard Betts", "Duane Allman", "Chuck Leavell", "Vassar Clements", "Johny Sandlin"],
  "Topics": ["music review", "album review"],
  "Organizations": [],
  "Artists": ["Richard Betts", "Allman Brothers Band"],
  "PublicFigures": [],
  "Events": []
}
```

### Example 3: Opinion Piece
```json
{
  "IssueDate": "1974-09-11",
  "IssueFile": "1974-09-11.pdf",
  "Type": "Article",
  "Section": "Opinions",
  "Title": "Now comes Jerry (President Gerald Ford)",
  "Page": 3,
  "Author": "GLENN HUGHES",
  "Names": ["GLENN HUGHES", "Gerald Ford", "Richard Nixon", "Elizabeth Bloomer"],
  "Topics": ["politics", "political commentary", "current events"],
  "Organizations": [],
  "Artists": [],
  "PublicFigures": ["Gerald Ford", "Richard Nixon"],
  "Events": []
}
```

### Example 4: Photo (NO AUTHOR)
```json
{
  "IssueDate": "1974-09-11",
  "IssueFile": "1974-09-11.pdf",
  "Type": "Photo",
  "Section": "The Spirit People",
  "Title": "Varsity Cheerleaders (Group Photo)",
  "Page": 11,
  "Author": "",
  "Names": ["Lynn Campbell", "Mary Powell", "Pam McGee", "Rita Hodges", "Pam Potter", "Pam Burkhalter", "Valerie Sheffield", "Pam Baxter", "Debbie Sasser", "Traci Talley"],
  "Topics": ["cheerleaders", "spirit squad"],
  "Organizations": ["Varsity Cheerleaders"],
  "Artists": [],
  "PublicFigures": [],
  "Events": []
}
```

### Example 5: Article with No Byline
```json
{
  "IssueDate": "1974-09-11",
  "IssueFile": "1974-09-11.pdf",
  "Type": "Article",
  "Section": "Hodge Podge",
  "Title": "Debate hosts tournament",
  "Page": 6,
  "Author": "",
  "Names": ["Mrs. Debbie Chapman", "Debbie Vest"],
  "Topics": ["debate", "speech"],
  "Organizations": ["Debate Team"],
  "Artists": [],
  "PublicFigures": [],
  "Events": ["September 20-21 Debate Tournament"]
}
```

## Your Task

Given the OCR text from [ISSUE DATE], generate complete JSON catalog entries for all articles and photos. Return ONLY valid JSON with no additional commentary.

Include the issue metadata at the start:
- IssueDate: [PROVIDED]
- IssueFile: [PROVIDED].pdf

Begin your JSON response now based on the following PDF attachment/link:
