# save_clipboard
#! python3
import shelve,pyperclip,sys
mcbShelf = shelve.open('mcb')

if len(sys.argv) == 3 and sys.argv[1].lower() == 'save': #save keywords and content
    mcbShelf[sys.argv[2]] = pyperclip.paste()

elif len (sys.argv) == 3 and sys.argv[1].lower() == 'delete': #delete keywords and content
    del mcbShelf[str(sys.argv[2])]
    
elif len(sys.argv) == 2:
    #list keywords and load content
    if sys.argv[1].lower() == 'list':
        pyperclip.copy(str(list(mcbShelf.keys())))
        print('now the keywords saved are '+ str(list(mcbShelf.keys())))
    elif sys.argv[1] in mcbShelf:
        pyperclip.copy(mcbShelf[sys.argv[1]])
        
mcbShelf.close()
