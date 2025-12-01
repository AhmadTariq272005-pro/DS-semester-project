 InsertWord(word)
Adds a new word at the end of Linked List
FUNCTION insertWord(word)
    CREATE newNode WITH value = word
    SET newNode.next = NULL
    IF head IS NULL THEN
        head = newNode
        RETURN
    ENDIF
    temp = head
    WHILE temp.next IS NOT NULL DO
        temp = temp.next
    ENDWHILE
    temp.next = newNode
END FUNCTION

FUNCTION 02
Insert At Position(position)
Insert word at specific index in the Linked List
FUNCTION insertAtPosition(word, position)
    CREATE newNode WITH value = word
    IF position == 1 THEN
        newNode.next = head
        head = newNode
        RETURN
    ENDIF
    temp = head
    FOR i = 1 TO position - 2 DO
        IF temp IS NULL THEN
            PRINT "Invalid Position"
            RETURN
        ENDIF
        temp = temp.next
    ENDFOR
    newNode.next = temp.next
    temp.next = newNode
END FUNCTION

FUNCTION 03
Delete Last Word
Removes last node from the Linked List and returns the word
FUNCTION deleteLastWord()
    IF head IS NULL THEN
        RETURN empty string
    ENDIF
    IF head.next IS NULL THEN
        word = head.word
        DELETE head
        head = NULL
        RETURN word
    ENDIF
    temp = head
    WHILE temp.next.next IS NOT NULL DO
        temp = temp.next
    ENDWHILE
    word = temp.next.word
    DELETE temp.next
    temp.next = NULL
    RETURN word
END FUNCTION

FUNCTION 04
Edit Word At Position(newWord)
Updates the word stored at specific node
FUNCTION editWordAtPosition(position, newWord)
    temp = head
    FOR i = 1 TO position - 1 DO
        IF temp IS NULL THEN
            PRINT "Invalid Position"
            RETURN
        ENDIF
        temp = temp.next
    ENDFOR
    temp.word = newWord
END FUNCTION

FUNCTION 05
Display Text Using Queue()
Displays all words in FIFO order using Queue
FUNCTION displayTextUsingQueue()
    CREATE empty queue q
    temp = head
    WHILE temp IS NOT NULL DO
        ENQUEUE temp.word INTO q
        temp = temp.next
    ENDWHILE
    IF q IS EMPTY THEN
        PRINT "(empty)"
        RETURN
    ENDIF
    PRINT "Text (Queue FIFO):"
    WHILE q IS NOT EMPTY DO
        PRINT FRONT(q)
        DEQUEUE q
    ENDWHILE
END FUNCTION
