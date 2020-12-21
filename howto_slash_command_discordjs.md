# Discord.js คำสั่ง "/"

ไฟล์ .MD อันนี้เป็นการสอนเบื้องต้นวิธีการเพิ่มอำนาจบอทในการสร้างคำสั่ง "/"
การสร้าง "/" และการรับเหตุการณ์การใช้ "/"

หากต้องการข้อมูลเพิ่มเติมสามารถเข้าไปอ่านได้ที่ [คู่มือดิสคอร์ดทางการ](https://discord.com/developers/docs/interactions/slash-commands)

การที่จะให้บอทสร้างคำสั่ง "/" ได้ บอทนั้นต้องมีอำนาจ `applications.commands`
โดยลิงก์ชวนบอทจะเป็น
`https://discord.com/api/oauth2/authorize?client_id=<ไอดีบอท>&scope=bot%20applications.commands`

หากใช้ Discord.JS เวอร์ชั่นล่าสุดอยู่แล้ว สามารถใช้งานได้เลย ไม่จำเป็นต้องมีการอัปเดตใด ๆ

## วิธีการสร้างคำสั่ง "/" :
สามารถสร้างคำสั่ง "/" ได้ทีละครั้งเท่านั้น สามารถนำไปประยุกต์ใช้ได้เอาเอง

### สร้างคำสั่ง "/" ในทุกดิส :
คำสั่งที่สร้างนี้จะขึ้นในทุกดิสที่บอทมีอำนาจในการสร้างคำสั่ง "/" แต่ใช้เวลานานกว่าจะปรากฎในทุกดิส
```js
client.api.applications(ค่าไอดีบอท).commands.post({data: {
    name: 'hello',
    description: 'ทักทายบอท'
}})
```

### สร้างคำสั่ง "/" เฉพาะดิสนั้น ๆ :
คำสั่ง "/" ที่สร้างจะขึ้นในดิสนั้น ๆ ทันที โดยไม่ต้องรอ
```js
client.api.applications(ค่าไอดีบอท).guilds(ค่าไอดีกิล/ดิส).commands.post({data: {
    name: 'hello',
    description: 'ทักทายบอท'
}})
```

## รับเหตุการณ์จากการใช้คำสั่ง "/" :
```js
client.ws.on('INTERACTION_CREATE', async interaction => {
  console.log(interaction);
})
```

## จัดการกับเหตุการณ์มีการใช้ "/" ที่รับมา :

เราจะใช้เงื่อนไขในการจัดการเหตุการณ์ที่รับมา โดยจากค่า ID หรือ ชื่อคำสั่งนั้น ๆ แล้วแต่ประยุกต์
```js
client.ws.on('INTERACTION_CREATE', async (interaction) => {
	if(interaction.data.name === 'hello') {
    console.log('HI !');
	}
});
```
