# Grocery App
Simple electron application created to quickly split groceries from receipts with friends, family, and significant others.
I just wanted something I could double click and start punching in lines.

## Usage
One string is entered with '[user] [item] [price]'
```
s milk 9.99
```

## Start
```
git clone https://github.com/fergusonB/groceries.git
npm install
npm run dev-electron
```

## Dev
```
    "dev-electron": "run-p dev start-electron",
    "build-electron": "run-s build start-electron",
    "start-electron": "electron ."
```

## Technology
Application in svelte - typescript / html / css
Electron wrapper (Yes, since you're wondering, I am aware this is overkill).


