# Dowl
Téléchargement des vidéos 
import express from "express";
import cors from "cors";
const app=express();
const PORT=process.env.PORT||10000;
app.use(cors({origin:process.env.ALLOWED_ORIGIN||"*"}));
app.use(express.json({limit:"20kb"}));
app.get("/",(_req,res)=>res.json({ok:true,service:"TokSave backend"}));
app.post("/resolve",(req,res)=>{
 const url=String(req.body?.url||"").trim();
 if(!/^https:\/\/(www\.)?(tiktok\.com|vm\.tiktok\.com)\//i.test(url))
   return res.status(400).json({error:"Invalid TikTok URL."});
 res.json({detected:true,sourceUrl:url,message:"Link detected. Configure an authorized media provider for content you own or have permission to download."});
});
app.listen(PORT,"0.0.0.0",()=>console.log(`Server listening on ${PORT}`));
