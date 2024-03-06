## Note Aggregation Tool

# Description

Tool for organizing and interlinking summarized notes from various sources.
Aims to create a dense, interconnected knowledge base, deduplicating notes
and presenting data transformations to spark connection between ideas.

# Features planned

- PostgreSQL database for note storage.
- Basic note creation and editing interface.
- Tag-based note categorization.
- Full-text search.
- Note 'obsoletion' for aggregation management.
- LLM integration for similarity suggestions.
- Note deduplication and smart versioning.
- Graph-based visualization of concept links.
- AI summarization of aggregated notes.
- Note evolution tracking (versioning).
- Collaborative editing and sharing.
- Import/export functionality (various formats).
- Integration potential with external tools.
- Analytics on note-taking patterns.

# Database structure design

### Notes Table
| Column Name    | Data Type                 | Constraints             |
|----------------|---------------------------|-------------------------|
| note_id        | SERIAL PRIMARY KEY       |                          |
| content        | TEXT                      |                         |
| creation_date  | TIMESTAMP                 |                         |
| last_modified  | TIMESTAMP                 |                         |
| obsolete       | BOOLEAN DEFAULT FALSE     |                         |
| source_book    | TEXT                      |                         |

### Tags Table
| Column Name    | Data Type                 | Constraints             |
|----------------|---------------------------|-------------------------|
| tag_id         | SERIAL PRIMARY KEY       |                          |
| tag_name       | TEXT UNIQUE               |                         |

### Notes_Tags (Many-to-many Relationship)
| Column Name    | Data Type                 | Constraints               |
|----------------|---------------------------|---------------------------|
| note_id        | INT FOREIGN KEY           | REFERENCES notes(note_id) |
| tag_id         | INT FOREIGN KEY           | REFERENCES tags(tag_id)   |

### Supporting Tables (Optional)

#### Aggregation History Table
| Column Name        | Data Type                 | Constraints               |
|--------------------|---------------------------|---------------------------|
| aggregation_id     | SERIAL PRIMARY KEY        |                           |
| original_note_id   | INT                       | REFERENCES notes(note_id) |
| aggregated_note_id | INT                       | REFERENCES notes(note_id) |
| aggregation_date   | TIMESTAMP                 |                           |
