```mermaid
flowchart TD
  %% Start
  Start([Start]) --> Identify[/"Identify interests & strengths:\nReflect on subjects & activities you enjoy and excel at."/]
  Identify --> PickMajor{{"Pick a major\n(Input: select from list)"}}
  PickMajor --> InitPot[/"Initialize Major Potential:\npotential = 0."/]

  %% Passion vs Skill
  InitPot --> AssessPassion["Assess Passion vs. Skill:\nIs this interest driven by passion or skill?"]
  AssessPassion --> PassionYes{"Passionate? (joyful about the work)"}
  AssessPassion --> PassionNo
  PassionNo -->|No| PickMajor
  PassionYes -->|Yes\npotential += 1| SkillCheck

  SkillCheck{"Are you good at this kind of work?"}
  PassionYes --> SkillCheck
  SkillCheck -->|Yes\npotential += 1| EvalJob
  SkillCheck -->|No\n(proceed anyway)| EvalJob

  %% Job prospects
  EvalJob["Evaluate job prospects:\nResearch career paths and job availability"] --> JobConf{"Are you reasonably confident you'll be able to get a job?"}
  JobConf -->|Yes\npotential += 1| Finances
  JobConf -->|No\npotential -= 1| Finances

  %% Financial stability
  Finances["Consider financial stability:\nResearch compensation for relevant roles"] --> MoneyConf{"Will you be able to stop living like a student once employed?"}
  MoneyConf -->|Yes\npotential += 1| LifeGoals
  MoneyConf -->|No\npotential -= 1| LifeGoals

  %% Life goals
  LifeGoals["Reflect on life goals:\nWhat do you truly want in life, regardless of career?"] --> GoalsConf{"Will a job from this major enable those life goals?"}
  GoalsConf -->|Yes\npotential += 1| EvalTotal
  GoalsConf -->|No| PickMajor

  %% Evaluate total
  EvalTotal["Evaluate total score:\n(Threshold used below: potential ≥ 4)"] --> Threshold{"Is potential ≥ 4?"}
  Threshold -->|Yes| AddToList["Process: majorList += thisMajor\n(major added to potential majors list)"]
  Threshold -->|No| PickMajor

  %% Consider other majors
  AddToList --> MoreMajors{"Do you want to consider any other majors?"}
  MoreMajors -->|Yes| PickMajor
  MoreMajors -->|No| AssessReqStart["Proceed to assess admission requirements\n(for each major in majorList)"]

  %% Admission requirements loop (process each major)
  AssessReqStart --> GetNextMajor{"Are there more majors on the list to process?"}
  GetNextMajor -->|Yes| SelectNext["Select next major from majorList\n(set currentMajor)"]
  GetNextMajor -->|No| End([End])

  SelectNext --> CheckReq["Assess admission requirements for currentMajor"]
  CheckReq --> MeetReq{"Do I meet the requirements for this major?"}
  MeetReq -->|Yes| KeepOnList["Keep on list (do nothing)"]
  MeetReq -->|No| CanMeet{"Can I meet the requirements before the deadline?"}
  CanMeet -->|Yes| KeepOnList2["Keep on list (plan to meet requirements)"]
  CanMeet -->|No| RemoveMajor["Remove currentMajor from majorList"]

  %% After decision, continue loop
  KeepOnList --> MoreOnList{"Are there more majors on the list to process?"}
  KeepOnList2 --> MoreOnList
  RemoveMajor --> MoreOnList

  MoreOnList -->|Yes| SelectNext
  MoreOnList -->|No| End

  %% End
  End --> Done([Finished processing majors])

  %% Styling / helpful notes (optional labels)
  classDef decision fill:#f9f,stroke:#333,stroke-width:1px;
  class PassionYes,SkillCheck,JobConf,MoneyConf,GoalsConf,Threshold,GetNextMajor,MeetReq,CanMeet,MoreMajors,MoreOnList decision;

5. **Commit changes**
