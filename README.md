# Localize.sh Proto

This repository contains the Protocol Buffers definitions for the **Localize.sh** toolchain. These schemas define the data structures for parsing, processing, and stringifying localization resources.

## Structure

*   **`localize/document.proto`**: Defines the `Document` structure, which represents a parsed resource file (AST + segments).
*   **`localize/segment.proto`**: Defines the `Segment` unit, representing a single translatable text unit with support for inline tags and attributes.
*   **`localize/processor.proto`**: Defines the request and response contracts for CLI processors (`Parse` and `Stringify` operations).

## Usage

These definitions are intended to be used with a CLI-based toolchain where processors read Protobuf messages from `stdin` and write to `stdout`.

### Data Flow

1.  **Parse**: `ParseRequest` (stdin) -> **Processor** -> `ParseResponse` (stdout)
2.  **Stringify**: `StringifyRequest` (stdin) -> **Processor** -> `StringifyResponse` (stdout)

## Definitions

### `Document`
A generic representation of a resource file.
*   `segments`: A list of translatable units found in the file.
*   `layout`: The Abstract Syntax Tree (AST) or structural representation of the original file (using `google.protobuf.Struct`).
*   `metadata`: Optional file-level metadata.

### `Segment`
A single unit of text for translation.
*   `id`: Unique identifier for the segment.
*   `text`: The content string, which may contain placeholder tags (e.g., `Hello {a1}World{/a1}`).
*   `tags`: A map of tag definitions corresponding to markers in the `text`.

### `Tag`
Attributes for a specific tag marker within a segment.
*   `attrs`: Key-value pairs of attributes for the tag (e.g., `href`, `style`).
