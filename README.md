import sqlite3

conn = sqlite3.connect('/Users/nautilus/Documents/Studying/Flask/my_study.db')
cur = conn.cursor()

wish = input ('Would you like to add a new word in your dictionary?:')

while wish == 'yes':
    user_word = input ('Please type a word:')
    user_value = input ('Please type a meaning:')
    cur.execute('INSERT INTO Dictionary (word, meaning) VALUES (?, ?)', 
    (user_word, user_value))
    print (user_word, user_value)
    

    answer = input ('Would you like to type one more meaning?:')

    while answer == 'yes':  

        user_value = input ('Please type another meaning:')

        cur.execute('INSERT INTO Dictionary (word, meaning) VALUES (?, ?)', (user_word, user_value))

        answer = input ('Would you like to type one more meaning?:')

    wish = input ('Would you like to add a new word in your dictionary?:')

cur.execute('SELECT word, meaning FROM Dictionary')
for row in cur:
     print(row)
        
conn.commit()
cur.close()
