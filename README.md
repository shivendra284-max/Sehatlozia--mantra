# Rebuilding the .aia with corrected JSON construction for MasterDetail screen
from zipfile import ZipFile
import os, json, shutil
project_dir = '/mnt/data/RoutineTrackerProject'
if os.path.exists(project_dir):
    shutil.rmtree(project_dir)
os.makedirs(f'{project_dir}/src/appinventor/ai_user/RoutineTracker', exist_ok=True)
os.makedirs(f'{project_dir}/youngandroidproject', exist_ok=True)

# Home screen JSON
home_props = {
    "YaVersion":"183","Source":"Form","Properties":{
        "$Name":"Screen1","$Type":"Form","Title":"Routine Tracker","AppName":"RoutineTracker","Uuid":"0",
        "BackgroundColor":"#121212","AlignHorizontal":"1","AlignVertical":"0",
        "Children":[
         {"$Name":"HeaderLabel","$Type":"Label","Text":"Routine Tracker","FontSize":"24","TextColor":"#FFFFFF"},
         {"$Name":"QuoteCard","$Type":"VerticalArrangement","Width":"FillParent","Height":"200","BackgroundColor":"#1E1E1E"},
         {"$Name":"QuoteLabel","$Type":"Label","Text":"Quote of the day will appear here.","FontSize":"16","TextColor":"#FFFFFF","Height":"200","Parent":"QuoteCard"},
         {"$Name":"WillpowerLabel","$Type":"Label","Text":"Willpower Score: 0","TextColor":"#FFFFFF"},
         {"$Name":"MasterListBtn","$Type":"Button","Text":"Open Master Tasks"},
         {"$Name":"QuotesManagerBtn","$Type":"Button","Text":"Manage Quotes"},
         {"$Name":"SettingsBtn","$Type":"Button","Text":"Settings"}
        ]
    }
}
scm_home = "#|\n$JSON\n" + json.dumps(home_props) + "\n|#"
with open(f'{project_dir}/src/appinventor/ai_user/RoutineTracker/Screen1.scm','w') as f:
    f.write(scm_home)

# MasterList screen
master_props = {
    "YaVersion":"183","Source":"Form","Properties":{
        "$Name":"MasterList","$Type":"Form","Title":"Master Tasks","AppName":"RoutineTracker","Uuid":"1",
        "BackgroundColor":"#121212","Children":[
         {"$Name":"AddMasterBox","$Type":"TextBox","Hint":"New master task name","TextColor":"#FFFFFF"},
         {"$Name":"AddMasterBtn","$Type":"Button","Text":"Add Master Task"},
         {"$Name":"MasterListView","$Type":"ListView","Elements":""},
         {"$Name":"BackBtn","$Type":"Button","Text":"Back"}
        ]
    }
}
scm_masterlist = "#|\n$JSON\n" + json.dumps(master_props) + "\n|#"
with open(f'{project_dir}/src/appinventor/ai_user/RoutineTracker/MasterList.scm','w') as f:
    f.write(scm_masterlist)

# MasterDetail with 20 subtasks
children = [{"$Name":"MasterTitle","$Type":"Label","Text":"Master Task Name","TextColor":"#FFFFFF"}]
for i in range(1,21):
    children.append({"$Name":f"SubLabel{i}","$Type":"TextBox","Hint":f"Subtask {i}","TextColor":"#FFFFFF"})
    children.append({"$Name":f"SubDone{i}","$Type":"CheckBox","Text":f"Done {i}","TextColor":"#FFFFFF"})
children.extend([{"$Name":"SaveMasterBtn","$Type":"Button","Text":"Save"},{"$Name":"BackBtn","$Type":"Button","Text":"Back"}])
masterdetail_props = {"YaVersion":"183","Source":"Form","Properties":{"$Name":"MasterDetail","$Type":"Form","Title":"Master Task","AppName":"RoutineTracker","Uuid":"2","BackgroundColor":"#121212","Children":children}}
scm_masterdetail = "#|\n$JSON\n" + json.dumps(masterdetail_props) + "\n|#"
with open(f'{project_dir}/src/appinventor/ai_user/RoutineTracker/MasterDetail.scm','w') as f:
    f.write(scm_masterdetail)

# Quotes Manager screen
quotes_props = {
    "YaVersion":"183","Source":"Form","Properties":{
        "$Name":"QuotesManager","$Type":"Form","Title":"Quotes Manager","AppName":"RoutineTracker","Uuid":"3",
        "BackgroundColor":"#121212","Children":[
         {"$Name":"AddQuoteBox","$Type":"TextBox","Hint":"Add a new quote","TextColor":"#FFFFFF"},
         {"$Name":"AddQuoteBtn","$Type":"Button","Text":"Add Quote"},
         {"$Name":"QuotesListView","$Type":"ListView","Elements":""},
         {"$Name":"BackBtn","$Type":"Button","Text":"Back"}
        ]
    }
}
scm_quotes = "#|\n$JSON\n" + json.dumps(quotes_props) + "\n|#"
with open(f'{project_dir}/src/appinventor/ai_user/RoutineTracker/QuotesManager.scm','w') as f:
    f.write(scm_quotes)

# Settings screen
settings_props = {
    "YaVersion":"183","Source":"Form","Properties":{
        "$Name":"Settings","$Type":"Form","Title":"Settings","AppName":"RoutineTracker","Uuid":"4",
        "BackgroundColor":"#121212","Children":[
         {"$Name":"ThemeLabel","$Type":"Label","Text":"Theme: Dark","TextColor":"#FFFFFF"},
         {"$Name":"ExportBtn","$Type":"Button","Text":"Export Data (CSV)"},
         {"$Name":"ImportBtn","$Type":"Button","Text":"Import Data"},
         {"$Name":"BackBtn","$Type":"Button","Text":"Back"}
        ]
    }
}
scm_settings = "#|\n$JSON\n" + json.dumps(settings_props) + "\n|#"
with open(f'{project_dir}/src/appinventor/ai_user/RoutineTracker/Settings.scm','w') as f:
    f.write(scm_settings)

# Project properties
project_properties = "main=Screen1\nname=RoutineTracker\nversioncode=1\nversionname=1.0\n"
with open(f'{project_dir}/youngandroidproject/project.properties','w') as f:
    f.write(project_properties)

# Create quotes.txt with 100 quotes (as before)
quotes = [
"Don’t watch the clock; do what it does. Keep going. — Sam Levenson",
"The future depends on what you do today. — Mahatma Gandhi",
"Don’t count the days, make the days count. — Muhammad Ali",
"Discipline is the bridge between goals and accomplishment. — Jim Rohn",
"Small daily improvements are the key to staggering long-term results. — James Clear",
"Do something today that your future self will thank you for.",
"You don’t have to be great to start, but you have to start to be great.",
"Success is the sum of small efforts, repeated day in and day out. — Robert Collier",
"The secret of getting ahead is getting started. — Mark Twain",
"Motivation is what gets you started. Habit is what keeps you going. — Jim Ryun",
"Start where you are. Use what you have. Do what you can. — Arthur Ashe",
"Action is the foundational key to all success. — Pablo Picasso",
"It always seems impossible until it’s done. — Nelson Mandela",
"Perseverance is not a long race; it is many short races one after the other. — Walter Elliot",
"Your limitation—it's only your imagination.",
"Push yourself, because no one else is going to do it for you.",
"Great things never come from comfort zones.",
"Dream it. Wish it. Do it.",
"Stay focused and never give up.",
"Don’t stop when you’re tired. Stop when you’re done.",
"The key to success is to focus our conscious mind on things we desire not things we fear. — Brian Tracy",
"Discipline is doing what needs to be done, even if you don’t want to. — Unknown",
"Make each day your masterpiece. — John Wooden",
"Strive for progress, not perfection.",
"The pain you feel today will be the strength you feel tomorrow.",
"Hard work beats talent when talent doesn’t work hard.",
"The difference between ordinary and extraordinary is that little extra.",
"Success usually comes to those who are too busy to be looking for it. — Henry David Thoreau",
"Make it happen.",
"Believe you can and you're halfway there. — Theodore Roosevelt",
"Don't wish for it. Work for it.",
"Act as if what you do makes a difference. It does. — William James",
"You miss 100% of the shots you don't take. — Wayne Gretzky",
"Don't be pushed around by the fears in your mind. Be led by the dreams in your heart.",
"Keep going. Be all in.",
"Either you run the day or the day runs you. — Jim Rohn",
"Opportunities don’t happen. You create them. — Chris Grosser",
"Be stronger than your strongest excuse.",
"If you want it, work for it.",
"Greatness starts with a decision to try.",
"Success is not for the lazy.",
"Take control of your habits, take control of your life.",
"Build routines that build you.",
"Consistency compounds.",
"Your future is created by what you do today, not tomorrow. — Robert Kiyosaki",
"The way to get started is to quit talking and begin doing. — Walt Disney",
"Be patient. Great things take time.",
"Discipline equals freedom. — Jocko Willink",
"Fall seven times, stand up eight. — Japanese Proverb",
"One day or day one. You decide.",
"Small deeds done are better than great deeds planned. — Peter Marshall",
"Make time your friend, not your enemy.",
"Focus on being productive instead of busy.",
"A year from now you will wish you had started today.",
"Do the hard things now so you can live the easy life later.",
"Progress is progress, no matter how small.",
"Turn your can’ts into cans and your dreams into plans.",
"Don't compare your chapter 1 to someone else's chapter 20.",
"Work hard in silence. Let success make the noise.",
"Discipline is choosing between what you want now and what you want most. — Abraham Lincoln",
"Good things come to those who hustle.",
"Success is the sum of details. — Harvey S. Firestone",
"Consistency is the true foundation of trust. Either keep your promises or do not make them.",
"Make discipline a habit.",
"The best way to predict the future is to create it. — Peter Drucker",
"Your only limit is you.",
"Start small. Think big.",
"Don't wait for opportunity. Create it.",
"The distance between dreams and reality is called action.",
"Don't fear failure. Fear being in the same place next year as you are today.",
"Success doesn't come to you, you go to it. — Marva Collins",
"Push past your limits.",
"Decide. Commit. Succeed.",
"Turn intentions into actions.",
"Keep your eyes on the stars, and your feet on the ground. — Theodore Roosevelt",
"Let your work speak for itself.",
"Make every day count.",
"Success is built daily.",
"Create a life you don't need a vacation from.",
"Master the little things.",
"Build momentum with consistency.",
"Sweat is just weakness leaving the body.",
"Persist until something happens.",
"Grind now, shine later.",
"One step at a time.",
"Focus on progress, not perfection.",
"Don't quit. Suffer now and live the rest of your life as a champion. — Muhammad Ali",
"Energy and persistence conquer all things. — Benjamin Franklin",
"Invest in yourself. It pays the best interest."
]
while len(quotes) < 100:
    quotes.append(f"Motivational quote #{len(quotes)+1}")

with open(f'{project_dir}/src/appinventor/ai_user/RoutineTracker/quotes.txt','w') as f:
    f.write("\n".join(quotes))

# Basic blocks placeholders
bky_placeholder = "<xml xmlns=\"http://www.w3.org/1999/xhtml\">\n  <block type=\"component_event\"></block>\n</xml>"
for screen in ["Screen1","MasterList","MasterDetail","QuotesManager","Settings"]:
    with open(f'{project_dir}/src/appinventor/ai_user/RoutineTracker/{screen}.bky','w') as f:
        f.write(bky_placeholder)

# Package into .aia
aia_path = '/mnt/data/RoutineTracker.aia'
with ZipFile(aia_path, 'w') as zipf:
    for root, dirs, files in os.walk(project_dir):
        for file in files:
            file_path = os.path.join(root, file)
            arcname = os.path.relpath(file_path, project_dir)
            zipf.write(file_path, arcname)

aia_path
