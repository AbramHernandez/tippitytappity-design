# tippitytappity-design

tippitytappity is a program to practice typing


## Data model

classDiagram
    User "1" -- "1" UserProfile
    UserProfile "1" o-- "many" Badge
    TypingSession "1" -- "1" TypingAnalyzer
    TypingSession "1" -- "1" WordBank

    class User{
        - name: string
        - email: string
        - password: string
        + login(user: string, pass: string) boolean
        + getEmail() string
    }

    class Badge{
        - title: string
        - description: string
        + awardCriteria(session: TypingSession)
    }

    class UserProfile{
        - badges: vector~Badge~
        + addBadge(badge: Badge)
        + getBadges() vector~Badge~
        + getRank() int
    }

    class TypingSession{
        - keystrokes: vector~char~
        - wordsTyped: vector~string~
        - startTime: datetime
        - endTime: datetime
        + start()
        + end()
        + recordKeystroke(k: char)
        + getElapsedTime() double
    }

    class TypingAnalyzer{
        + calcWPM(session: TypingSession) double
        + calcAccuracy(session: TypingSession) float
        + getRank(session: TypingSession) int
    }

    class WordBank{
        - words: vector~string~
        + loadWords(source: string)
        + getRandomWord() string
        + getPhrase(length: int) vector~string~
    }