# Specification Phase Exercise

A little exercise to get started with the specification phase of the software development lifecycle. In this exercise, your team specifies a set of improvements and new features for [The Slide Machine](https://theslidemachine.com) — see the [instructions](instructions.md) for detail, and the [background](background.md) for an introduction to the software product you are tasked with extending.

## Team members
Monica Lee  https://github.com/monica9482  
Yusef Moustafa  https://github.com/YusefMoustafa  
Leslie Sampaney  https://github.com/Leslie-Sampaney  
Krishiv Seth  https://github.com/krishivseth   
Veer Singh  https://github.com/sing1179  

## Review of the Current Application
Strengths:  
- Mostly accurate transcriptions of speech onto slides  
- Navigation cue words to go forward and back a slide  
- Verbally add a picture to a given slide  
- Filler words or stutters ignored for non-strong speakers  
- AI accurately predicts and completes sentences most of the time
- Acronyms like SDLC and CI/CD came out spelled correctly, and a long stretch about waterfall versus agile became a clean two column comparison slide
- Before a quiz is published, a review screen lets the instructor edit every question and set points for each one
- Quiz settings let the instructor choose the number of questions, the question types, and add extra instructions for the AI

Weaknesses:  
- Image resource pool/must be seeded pre-lecture  
- Design template importing is not the best  
- New slide predictor doesn't allow for gaps/pauses for non-strong speakers
- Saying "next slide" mid lecture added a blank slide (slide 10) with no title or text that stayed in the finished deck
- Maintenance was said out loud but appears on none of the 12 slides, and the summary slide says six phases while the phase list slides only show five
- AI freedom defaults to 2 out of 5, so slides can include content the instructor did not say, and quizzes are written from the slide text by default with the spoken transcript as an unchecked box
- Opening a quiz link with a personal Gmail account showed "You need access" with no explanation    

Gaps:  
- Real-time verbal correction  
- Editing/approving material during the lecture  
- Unable to verbally insert diagrams/charts/graphs  
- Unable to verbally link words   
- Unable to add videos
- Signed out, the lecture page shows only the slides, a play button, and language and share icons, with no place to ask about a slide, no definitions of terms, and no mention that a quiz exists
- Quiz settings never say which accounts can open the quiz, and nothing warns the instructor before publishing
- After publishing, the Quiz tab shows only a Google Forms link, a copy button, and Delete quiz, with no open or close time and no way for students to reach it

## Prior Art & Originality

On September 29, 2026 we read the Software Design Document sections 18 (Future Work) and 19 (Open Questions), docs/ROADMAP.md including its section 9 cut line, all 37 open issues on bloombar/slide-machine, and the pull request list (0 open, 204 closed). We also read the requirement IDs closest to our idea, PREP-1 to PREP-4, QUIZ-1 and QUIZ-2, EVAL-5, SOC-1, SHARE-1 and SHARE-2, and section 16 on privacy.

Nothing in Future Work, Open Questions, the roadmap, or the issue tracker specifies a glossary for students or a way for students to ask a question on a slide. Future Work lists eight items (local models, live translation, extracting the STT pipeline, an MCP server, collaborative editing, seat-based billing, analytics dashboards, a faculty setup guide). The open issues are spec-tracking issues for templates, preflight, evaluation, billing and privacy, one narration bug (#230), and three older ideas, required transcript viewing with quiz questions mid-slideshow (#27), export (#26), and pre-fetching seed content (#5). Issue #27 goes the other direction from ours. The instructor asks the students questions there. In ours the students ask.

Three existing things sit close to our proposal, and we built on them rather than around them.

PREP-1 and PREP-2 already have the AI extract key terms, acronyms and a short gloss from seed material before a lecture, for the instructor to prune and disambiguate. That list exists to steer generation and speech recognition and students never see it. Our glossary starts from the same extraction but runs after the lecture on what was actually said, adds an approve, edit, hold, discard state per term, shows the slide text each definition came from, and puts the approved result in front of students on the slide itself. The student-facing half and the approval gate are new.

QUIZ-1 and QUIZ-2 set the pattern where the AI drafts, the instructor reviews every item, then publishes. We copied that pattern on purpose for definitions and answers, and we put both new tabs next to Quiz in Lecture settings so the instructor meets the same workflow in the same place. The pattern is prior art. Applying it to student questions is ours.

EVAL-5 describes a per-slide relevance rating from students and then declines to build it for the pilot, putting the rating inside the exit ticket instead. Our "where students asked" strip on the Questions tab is not a rating. It counts real questions per slide. It gives the instructor the confusion signal EVAL-5 wanted, as a byproduct of answering questions, at no extra cost per lecture.

Two constraints from section 16 shaped the design. A question a student types is student data, so the draft request sends the model only the question text and the slide text, never the student's name or email, and a student can post anonymously to the instructor as well. Every AI draft is metered against the instructor's AI generation allowance under BILL-3, the same as a quiz, and both new tabs show the plan limit message when the cap binds.

What is new in this proposal is the student-facing glossary anchored to slide terms, the slide-by-slide question area with instructor approval before anything is shown, AI drafts that display the slide text they used, per-slide question counts, and carry-over of approved terms and answers to a later lecture with student names removed.

## Stakeholders

Students:  
**Student A, Student participant**  
Background: Student; Senior and Business.  
Interview method: Interview about study habits and proposed features, followed by app-use tasks directly observed by a team member.  
Goals and needs:  
- Understand lecture material using slides and professor-provided notes.
- Find explanations of unfamiliar terminology.
- Revisit prerequisite concepts through textbook material.
- Obtain clarification from professors, friends, office hours, or an LLM.
- Know whether an answer has been reviewed by an instructor before relying on it.

Problems and concerns:  
- Described encountering confusing slides and seeking clarification through LLMs.
- Needs to consult additional sources when terminology or prerequisite concepts are unfamiliar.
- Would not trust a classmate’s answer before professor review.
- Checks suspected errors with the professor.
- Would be uncomfortable with instructors seeing that they sought help from outside sources.

Observed app use and participant comments:  
- Selected a lecture because it seemed interesting.
- Used Google to investigate unfamiliar terminology and found sufficient, useful information.
- Successfully returning to an earlier explanation using memory.
- Said that a clarification request should include surrounding context and relevant material.

Reactions to proposed features:  
- Responded positively to an embedded glossary, particularly explanations that break down complex topics.
- Identified professor review as a condition for trusting peer answers in a slide-specific Q&A feature.  

Limitations:  
- The concept-understanding task was skipped.
- Successful Google use does not establish that external lookup is a problem.
- The participant did not test a glossary or Q&A prototype.
- Discomfort with disclosure of outside help does not establish their preference about aggregate in-app statistics.
  
**Student B, Student participant**  
Background: Student; Grad level and Industrial Engineering.  
Interview method: Interview about study habits and proposed features, followed by app-use tasks directly observed by a team member.  
Goals and needs:  
- Study using lecture slides and past exam papers.
- Obtain clarification through office hours or a teaching assistant.
- Understand unfamiliar terms and prerequisite concepts using Google or an LLM.
- Locate earlier explanations when revisiting lecture material.
- Distinguish instructor-reviewed answers from unchecked peer responses.  

Problems and concerns:  
- Described seeking help when lecture slides are confusing.
- Needs additional explanations for unfamiliar terminology and prerequisite concepts.
- Faced difficulty finding an earlier explanation in the deck.
- Would not trust a classmate’s answer before professor review.
- Would be uncomfortable with instructors seeing that they sought help from outside sources.  

Observed app use and participant comments:  
- Selected the first lecture they could find.
- Used an LLM to investigate unfamiliar terminology and found it useful.
- Had difficulty locating an earlier explanation and said they did not know where to find it.
- Said that a clarification request should include surrounding context, relevant material, and their current understanding.
- Described explaining a concept in simple words as a personal check of understanding; this ability was not demonstrated during the tasks.  

Reactions to proposed features:  
- Responded enthusiastically to the embedded glossary idea.
- Initially suggested that an answer remaining online indicated trustworthiness, but clarified that professor review would be necessary before trusting a classmate’s answer.  

Limitations:  
- The concept-understanding task was skipped.
- The specific navigation steps that led to difficulty.
- Positive reactions to the glossary do not demonstrate its effectiveness; no prototype was tested.
- Their preference concerning aggregate in-app statistics remains unknown.


Instructors and TAs:

**TA A, teaching assistant participant**

Note: TA A is a teaching assistant, not the instructor of record. We interviewed him because he answers student questions about lecture slides and reviews course material.

Background: Teaching assistant for a course that uses Ruby on Rails. Worked with about 48 to 50 students last semester and 70 this semester. The course slides come from another school's curriculum.

Interview method: Video call interview about how students ask for help, followed by app tasks done while sharing his screen from his phone, observed by a team member.

Goals and needs:
- Give students homework support, especially with Git and GitHub, such as which branch to merge into, writing pull request descriptions, and who is responsible for merging.
- Answer common setup questions quickly, such as Ruby on Rails on Windows.
- Keep lecture slides accurate, up to date, and in line with the curriculum, since students study from the slides first before exams.
- Check any AI written answer against the course textbook before it reaches students, since it is still his job to make sure it is correct.
- Prefers slides with bold definitions and bullet points over long paragraphs.
- Values student questions and would spend at least 1 to 2 hours a week on them, possibly up to 4.

Problems and concerns:
- Students often struggle with Git and GitHub. Some open pull requests with no description, and merge responsibility is confusing.
- The same questions come back semester after semester, such as Windows setup for Ruby on Rails, though they are not usually repeated within one semester.
- Students usually email first. He described their usual path as ask AI, then post on EdStem, then set up Zoom or come in person if still confused.
- Said he has never had a student ask a question that is directly on the slides or syllabus. Students come to office hours having tried other options first.
- Found slide 9 too wordy, like a small paragraph, and noted it does not mention arrange, act, assert, which is a concept he would ask about.
- Would not approve an AI drafted answer if it is generated without showing where it came from.
- Would not review student questions during class because changes to content slides have to match the curriculum.

Observed app use and participant comments:
- Found slide 9 (unit tests) in about 20 seconds by swiping through the deck on his phone.
- Asked what he would do as a student confused by slide 9 with no professor to ask, he said he would wait for a break or ask at the end. He did not mention looking for a way to ask inside the app.
- Asked how he would add a definition as the instructor, he said he would make it bold or clearly marked and use bullet points. He described this and did not try it in the app.

Reactions to proposed features:
- Student questions posted on a slide and shown only after instructor approval: called students' questions "very valuable." Would review them on his own time or during office hours, not in class.
- AI drafted answers: would approve them only if the draft shows the resource it pulls from, such as a textbook citation he could check. Said no to blind generation.

Limitations:
- One TA, not an instructor. His course slides are described as very complete, so his experience may differ in other courses.
- His statement that students do not ask about things covered on the slides gives no support to a glossary of terms.
- Not asked about the glossary, anonymous or named questions, or where questions are stored.
- Some questions were leading, such as asking if he would put a definition "straight on the slide" and whether he would review "during class."
- The task of spotting problems in the deck was not run.
- Time estimates are self reported, and he said it "depends."
- He swiped on a phone instead of using the desktop view.
- Reactions were to a spoken description, not a prototype.

**Instructor A, instructor participant**

Background: Math instructor who teaches calculus and discrete math to about 50 students.

Interview method: Interview about how students ask for help, followed by app tasks with a sample lecture deck, observed by a team member.

Goals and needs:
- Answer student questions in class, and by email when students ask outside class hours.
- Have lecture slides that students can follow without prior knowledge, with acronyms explained.
- Keep the design of the slides consistent.
- Find out earlier that students were confused instead of learning it from exam grades.
- Values student questions and would spend about an hour a week reviewing them, before and after class.
- Wants to read and edit any AI drafted answer before students see it.

Problems and concerns:
- Learns that students were confused only after the exam, from their grades.
- Students who have a question outside class hours have to email him.
- Students often ask the same questions again, semester after semester.
- Said students often search for answers themselves instead of asking.
- Said the sample deck had inconsistent fonts, a missing slide, acronyms that were not explained, and assumed prior knowledge.
- Worries an AI drafted answer might not be accurate.

Observed app use and participant comments:
- Looked through the deck and pointed out the inconsistent font, unexplained acronyms, assumed prior knowledge, and a missing slide.
- Found slide 9 (unit tests) in about 20 seconds by swiping through the slides.
- Asked what a confused student could do from the page, he said they would email him and that there is no way to ask on the screen.

Reactions to proposed features:
- Student questions posted on a slide and shown only after instructor approval: yes, he would review them because student questions are important, for about an hour a week, before and after class.
- Anonymity: would rather each student chooses whether to post anonymously or not.
- AI drafted answers: would need to read and edit them in case they are not accurate.
- Showing questions from earlier semesters: yes, because similar questions come up each time.

Limitations:
- Answers were short and some questions were not answered, such as which terms students get stuck on and what would make him not use the feature.
- The interviewer knows the participant personally.
- Reactions were to a spoken description, not a prototype.
- Time estimates are self reported.
- His experience with math courses may differ from other subjects.

## Product Vision Statement

The Slide Machine gets an instructor reviewed glossary and slide by slide question area, where the AI drafts definitions and answers, the instructor approves, edits, holds, or discards each one, and students see only what was approved, so a student gets trusted help on the exact slide that confused them.

## User Requirements

Students
1. As a student, I want to open a course-specific definition directly from an unfamiliar term on a slide so that I can understand it while studying.
2. As a student, I want definitions to include simple explanations and examples so that complex terminology is easier to understand.
3. As a student, I want to search the glossary for a term so that I can find its meaning without remembering where it appeared.
4. As a student, I want an explanation to link to relevant prerequisite terms or earlier course material so that I can revisit background knowledge I need.
5. As a student, I want to return to my original slide after consulting an explanation so that I can continue studying without losing my place.
6. As a student, I want to find questions and answers associated with a slide so that I can check whether they address my confusion.
7. As a student, I want my question to include a reference to the slide so that the person answering can see the relevant context.
8. As a student, I want to describe what I currently understand when asking a question so that the response addresses the part I am struggling with.
9. As a student, I want to identify answers reviewed by the professor so that I know which explanations I can rely on.
10. As a student, I want to request further clarification when an explanation is insufficient so that I can resolve what remains unclear.
    
Instructors

1. As an instructor, I want the app to suggest definitions for the hard terms and acronyms in my lecture so that I don't have to write every definition myself.
2. As an instructor, I want to approve, edit, hold, or discard each suggested definition so that students only see wording I trust.
3. As an instructor, I want each suggested definition to show the slide or transcript text it came from so that I can check that it is accurate.
4. As an instructor, I want to change or remove a definition after students can see it so that I can fix a mistake quickly.
5. As an instructor, I want to see all new student questions in one list grouped by slide so that I can review them in one sitting.
6. As an instructor, I want a student question to stay hidden from other students until I approve an answer so that a wrong answer never reaches the class.
7. As an instructor, I want the app to draft an answer to a student question and show the slide text it used so that I can check it and edit it before I approve it.
8. As an instructor, I want approved questions and answers from earlier semesters to carry over to my next class with no student names so that I don't answer the same question every term.
9. As an instructor, I want to see how many questions each slide received so that I can find where students were confused before the exam.
10. As an instructor, I want a clear message when the app cannot draft an answer, for example when the AI is unavailable or my usage limit is reached, so that I know to write it myself and don't wonder what went wrong.
11. As an instructor, I want to write an answer myself instead of using the AI draft so that I can answer in my own words or when the AI is not available.
12. As an instructor, I want to hide an approved answer so that I can pull it back if I find a mistake.
13. As an instructor, I want to discard a student question that is off topic so that it never shows to other students.
14. As an instructor, I want a notice on the lecture page when new student questions are waiting so that I know when to review them.

## Activity Diagrams

![instructor story 2](story2.png)  
As an instructor, I want to approve, edit, hold, or discard each suggested definition so that students only see wording I trust.  
  
![instructor story 7](story7.png)  
As an instructor, I want the app to draft an answer to a student question and show the slide text it used so that I can check it and edit it before I approve it.  
  
![student story 3](story3.png)  
As a student, I want to search the glossary for a term so that I can find its meaning without remembering where it appeared.  
  
![student story 6](story6.png)  
As a student, I want to find questions and answers associated with a slide so that I can check whether they address my confusion.  

## Wireframes

Every screen the proposal adds or changes, for both user types. Changed screens are screenshots of the live app (taken September 30, 2026, on a lecture in Krishiv's account and on Monica's Biology deck as a viewer) with the new parts drawn on top. New screens are plain boxes. A dashed outline marks what is new or changed and the numbered notes under each image say what it is.

Where things live. Instructor review happens in two new tabs of the existing Lecture settings modal, Glossary and Questions, placed right after Quiz. That is where the app already puts AI work the instructor checks before students see it (Quiz has generate, review, publish, and Refine with AI works the same way). Students get everything on the lecture page they already open from the shared link. Reading the glossary and the approved answers needs no account. Asking a question does, through the app's existing "Log in to" gate, so names stay inside the app and a student can pick anonymous per question.

The same screens are in Figma with the click-through wired, linked in the Clickable Prototype section.

### Instructor screens

#### Instructor 1. Lecture page (owner) (changed screen)

![Lecture page (owner)](wireframes/png/i-lecture.png)

- (1) Notice under the nav with the count of new student questions. Review opens Lecture settings on the Questions tab.
- (2) Small tag on each slide with its question count. Opens the Questions tab filtered to that slide.
- (3) Two new items at the bottom of the slide menu.
- Rest of the page is unchanged.

Covers user stories Instructor 5 and Instructor 9.

#### Instructor 2. Lecture settings, Glossary tab (new screen)

![Lecture settings, Glossary tab](wireframes/png/i-glossary.png)

- (1) New tab next to Quiz. Other tabs unchanged.
- (2) Suggest definitions asks the AI for hard terms and acronyms from the slides and transcript. Add a term is manual.
- (3) Carry over reuses approved terms from an earlier lecture.
- (4) Each row: term, definition, which slide it came from, status, and Approve / Edit / Hold / Discard. Approved rows get Hide instead, so a bad one can be pulled later.

Covers user stories Instructor 1, Instructor 2, Instructor 3, Instructor 4 and Instructor 8.

#### Instructor 3. Glossary tab, editing one definition (new screen)

![Glossary tab, editing one definition](wireframes/png/i-glossary-edit.png)

- (1) Row expands. Term, definition, optional example, optional related terms.
- (2) Slide text it came from stays visible while editing.
- (3) Save = approve (students see it) or keep on hold. Cancel drops the edit.

Covers user stories Instructor 2, Instructor 3, Instructor 4, Student 2 and Student 4.

#### Instructor 4. Lecture settings, Questions tab (new screen)

![Lecture settings, Questions tab](wireframes/png/i-questions.png)

- (1) New tab. All student questions on this lecture in one list, grouped by slide.
- (2) Bar per slide = how many questions it got. Click one to filter.
- (3) No answer yet: Draft an answer with AI, or Write it myself. Nothing is shown to other students until Approve.
- (4) Questions carried over from an earlier class come with no name.

Covers user stories Instructor 5, Instructor 6, Instructor 7, Instructor 8 and Instructor 9.

#### Instructor 5. Questions tab, reviewing one question (new screen)

![Questions tab, reviewing one question](wireframes/png/i-question-review.png)

- (1) Left: the question, the slide, and what the student said they understand.
- (2) Right: the AI draft (editable) and the slide text it used, with the bits it relied on marked. TA A said he would not approve a draft without this.
- (3) Approve publishes under the slide. Save on hold keeps the edit hidden. Discard / Cancel.

Covers user stories Instructor 6, Instructor 7, Student 7 and Student 8.

#### Instructor 6. Questions tab, error states (AI down, plan limit, offline) (new screen)

![Questions tab, error states (AI down, plan limit, offline)](wireframes/png/i-errors.png)

- (1) AI provider refused or timed out. Answer field stays empty and ready to type in.
- (2) Plan AI allowance used up. See usage goes to Account settings, Plan & Usage (exists today).
- (3) Approve/Save did not reach the server. Edit is kept, Retry resends. Same banners on the Glossary tab.

Covers user stories Instructor 10, Instructor 2 and Instructor 7.

#### Instructor 7. Carry over from an earlier lecture (new screen)

![Carry over from an earlier lecture](wireframes/png/i-carry-over.png)

- (1) Pick one of your earlier lectures and what to bring over.
- (2) Student names are removed. Carried questions show as "from an earlier class". Only approved items come across.

Covers user stories Instructor 8.

### Student screens

#### Student 1. Shared lecture page (signed out) (changed screen)

![Shared lecture page (signed out)](wireframes/png/s-lecture.png)

- (1) Glossary button in the nav, next to the language switcher.
- (2) Terms with an approved definition get a dotted underline on the slide. Click one to see the definition.
- (3) Questions area under the slide. Count of approved answers, and Ask about this slide (needs sign in).
- Slides, play, language, share and full screen are as today.

Covers user stories Student 1, Student 6 and Student 9.

#### Student 2. Definition popover on a term (new screen)

![Definition popover on a term](wireframes/png/s-term.png)

- (1) Click the underlined term, a small box opens next to it. Close (x, Esc, or click the slide) and you are back where you were.
- (2) Definition, example, related terms (each opens its own box), and the reviewed mark.
- (3) Open full glossary goes to the Glossary panel.

Covers user stories Student 1, Student 2, Student 4 and Student 5.

#### Student 3. Glossary panel (new screen)

![Glossary panel](wireframes/png/s-glossary.png)

- (1) Panel beside the slides. Search filters as you type.
- (2) Each term says which slide it is on. Go to slide jumps there and keeps the panel open.
- (3) Footer says everything here was approved by the instructor.

Covers user stories Student 1, Student 3, Student 4 and Student 5.

#### Student 4. Questions on this slide (new screen)

![Questions on this slide](wireframes/png/s-questions.png)

- (1) Only approved questions and answers show, each with the reviewed mark.
- (2) Ask a follow-up on any answer when it is not enough.
- (3) Signed in: your own questions show at the top with their status (waiting / answered). Signed out you just see the approved list and a sign in prompt on Ask.

Covers user stories Student 6, Student 9 and Student 10.

#### Student 5. Ask about this slide (signed in) (new screen)

![Ask about this slide (signed in)](wireframes/png/s-ask.png)

- (1) The slide is attached automatically.
- (2) Question + optional "what you understand so far". Post as your name or anonymous, per question.
- (3) If the send fails the text stays and you get Try again. A follow-up uses this same form with the earlier answer attached.

Covers user stories Student 7, Student 8, Student 9 and Student 10.

#### Student 6. Sign in to ask (existing dialog, new title) (changed screen)

![Sign in to ask (existing dialog, new title)](wireframes/png/s-signin.png)

- (1) Reuses the app's existing "Log in to..." dialog. Same Google / email form.
- (2) One line says why. After sign in you land on the Ask form for the same slide. Reading never needs an account.

Covers user stories Student 7 and Student 9.  

## Clickable Prototype

Figma prototype, no login needed to view. https://www.figma.com/proto/N6brbXDTkaKgmOEjn25Oaz

Two flows are set up in the file. Instructor starts on the lecture page signed in as the owner. Student starts on the shared lecture page signed out. Every button and link in every frame goes to the next screen, including the error states. The design file itself is at https://www.figma.com/design/N6brbXDTkaKgmOEjn25Oaz.

Backup copy of the same click-through as a plain HTML page, in case Figma is down during the demo. Open [`wireframes/wireframes.html`](wireframes/wireframes.html) and switch to Click-through at the top.

## Stakeholder Demo

* [Generated slide deck](https://theslidemachine.com/d/untitled-23b2c524)
* [Recorded demo](https://drive.google.com/file/d/1LAmA76tiIZcntYFAi5zq9ooB3ZyogpM_/view?usp=sharing)
## Exit Ticket

* [Exit ticket quiz](https://docs.google.com/forms/d/e/1FAIpQLSecNVSDyQymAAdv-oCcyd5D-unaGXXQovK15xpeFIq0oiVAOA/viewform)
