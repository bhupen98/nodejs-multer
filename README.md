### Installation 
``` terminal
yarn add multer
```

### Usage
``` javascript
const multer = require('multer');

// for file type support 
// for file type support 
const MIME_TYPE_MAP = {
    'image/png':'png',
    'image/jpeg':'jpg',
    'image/jpg':'jpg'
}

const storage = multer.diskStorage({
    destination:(req,file,callback)=>{
        const isValid = MIME_TYPE_MAP[file.mimetype];
        let error = new Error("Invalid mime type");
        if(isValid){
            error=null;
        }
          callback(error,"images")
    },

    filename:(req,file,callback)=>{
        const name = file.originalname.toLowerCase().split(' ').join('-'); // it will miss the file type
        const ext = MIME_TYPE_MAP[file.mimetype];
        callback(null,name+'-'+Date.now()+'.'+ext)
    }
});
```
