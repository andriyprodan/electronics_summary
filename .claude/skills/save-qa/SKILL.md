---
name: save-qa
description: Save the current Q&A discussion (user's questions + Claude's answers) as a separate markdown note inside a lesson folder, and insert a relative link to it into that lesson's summary.md at the user's cursor/selection. Use when the user asks to "додай до уроку N те, що ми проговорили", save the conversation to a lesson, or similar.
---

# Save Q&A discussion to a lesson

## Steps

1. **Find the lesson folder.** Lessons live under `The Complete Electronics Course. Analog Hardware Design/Section */Урок N. .../`. Each has a `summary.md` plus images. Locate it with `find` by lesson number.

2. **Create the Q&A file** in that lesson folder:
   - Name: `Питання. <Коротка тема>.md` (Ukrainian, short topic, e.g. `Питання. Напруга, робота і потужність.md`).
   - First line: `# Питання. <Коротка тема>`, then a back-link `[← Назад до уроку N](summary.md)`.
   - One `## <номер>. <суть питання>` section per user question, in order.
   - Under each heading, the user's question **verbatim** as a blockquote: `> **Питання:** ...` (keep their wording and typos).
   - Then Claude's answer, keeping its substance and structure (subheadings, tables, formulas in `$...$` / `$$...$$`).
   - Per [Agents.md](../../../Agents.md): after formulas, add descriptions of variables with units (`де: - $U$ — напруга, В; ...`) where they are not obvious. Do not otherwise pad the prose.

3. **Insert the link into `summary.md`** at the user's cursor / IDE selection (the `ide_selection` line). If they left an empty placeholder like `()`, fill it: `(див. [<Назва>](<файл>))`. Otherwise insert `(див. [<Назва>](<файл>))` at that spot.
   - Link path is relative to `summary.md` (same folder), with spaces encoded as `%20`; Cyrillic and commas stay as-is. Example:
     `[Питання. Напруга, робота і потужність](Питання.%20Напруга,%20робота%20і%20потужність.md)`

4. Do not commit unless the user asks. Report the created file and the inserted link.
