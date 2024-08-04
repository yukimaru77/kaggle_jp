# Help! Stuck in Kaggle's file import

**Andres H. Zapke** *Fri Jun 07 2024 18:40:39 GMT+0900 (日本標準時)* (1 votes)

Following the tutorial, I have a notebook and the following file structure (see Image).  This graphical interface is a bit misleading, main.py is inside of submission folder, not inside the lib folder.

So I run the game from my Kaggle notebook with game_output = env.run(agents=[simple_agent, simple_agent, simple_agent , "/kaggle/working/submission/main.py"]) and everything works until now.

However now "main.py" needs some methods of the "gemma" module. I tried importing them with sys.path.insert(0, "/kaggle/working/submission/lib")
    sys.path.insert(0, "./lib") and from gemma.config import * but I always get: "No module named 'gemma.config'".

I confirmed that gemma has an "init.py" file and I can't figure out how to import its methods into my main. Any tips appreciated!!

[Captura de pantalla 2024-06-07 a las 11.34.58.png](https://storage.googleapis.com/kaggle-forum-message-attachments/2859842/20789/Captura de pantalla 2024-06-07 a las 11.34.58.png)

