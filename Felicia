import discord
from discord.ext import commands
import asyncio
import random
from datetime import timedelta

# เปิดใช้งาน Intents
intents = discord.Intents.default()
intents.message_content = True

# ตั้งค่าบอท
bot = commands.Bot(command_prefix='!', intents=intents)

# กำหนดคำที่ไม่เหมาะสม
BAD_WORDS = [
    "ควย", "หี", "เย็ด", "กระหรี่", "งานกาก", "รูปกาก", "ลูกอีหน่อแตด", 
    "https://discord.com", "https://discord.gg", "nigga", "nigger", "NIGGERS"
]

# ใช้ set เพื่อเก็บข้อความที่เคยได้รับการจัดการแล้ว
processed_messages = set()

@bot.event
async def on_ready():
    print(f'บอทออนไลน์แล้วค่ะ! ชื่อ: {bot.user.name} (ID: {bot.user.id})')

@bot.event
async def on_message(message):
    if message.author == bot.user or message.id in processed_messages:
        return

    # ตรวจสอบคำไม่เหมาะสม
    if any(bad_word in message.content.lower() for bad_word in BAD_WORDS):
        messages_to_delete = [message]
        reply_message = await message.reply(
            f"คุณลูกค้า {message.author.mention} พูดจาแบบนี้ต้องโดนกักบริเวณนะคะ", mention_author=True)
        messages_to_delete.append(reply_message)
        await asyncio.sleep(1)

        countdown_messages = ["3", "2", "1", "ตู้ม✨️"]
        for text in countdown_messages:
            countdown_message = await message.channel.send(text)
            messages_to_delete.append(countdown_message)
            await asyncio.sleep(0.3)

        for msg in messages_to_delete:
            await msg.delete()

        processed_messages.add(message.id)

        try:
            timeout_duration = timedelta(minutes=1)
            await message.author.timeout(timeout_duration, reason="ใช้คำไม่เหมาะสม")
            random_number = random.randint(1, 100)

            if random_number <= 70:
                notify_message = await message.channel.send(
                    f"คุณลูกค้า {message.author.mention} โดนกักบริเวณ 1 นาทีเพราะทำตัวไม่น่ารัก!")
            elif random_number <= 90:
                notify_message = await message.channel.send(
                    f"{message.author.mention} เด็กดื้อต้องโดนอะไรน้าาา")
            else:
                notify_message = await message.channel.send(
                    f"ไอ้ลูกค้า {message.author.mention} โดนกักบริเวณ 1 นาที")

            await asyncio.sleep(3)
            await notify_message.delete()

        except Exception as e:
            print(f"ไม่สามารถ Timeout สมาชิกได้: {e}")

    # ตรวจสอบข้อความที่กำหนดเอง
    responses = {
        'มะเขือเทศบนข้าวผัดอร่อยดีนะ': "เดี๋ยวกูฆ่าตายเลย พูดบ้าอะไรวะ",
        'ไข่เจียวอร่อย': "ไข่ดาวอร่อยกว่า",
        'ขอดูรูจีบที่รูตูดหน่อยสิ': "คืนนี้คงได้มีคนตายคาตวยชั้นแล้วล่ะ",
        'แง': "กอดๆ",
        '/e โตงเตง': "เย่~~~",
        '/eโตงเตง': "เย่~~~",
        'เฟลิเซียขอดูเท้าหน่อย': "บ่นเหี้ยไรไอมืด",
        'feliciaขอดูเท้าหน่อย': "บ่นเหี้ยไรไอดำ",
        'เฟลิเซียขอเลียรักแร้หน่อยสิ': "บ่นเหี้ยไรไอมืด",
        'feliciaขอเลียรักแร้หน่อยสิ': "บ่นเหี้ยไรไอดำ",
        'เฟลิเซียขอลวนลามหน่อย': "บ่นเหี้ยไรไอมืด",
        'felicia show me your tips': "บ่นเหี้ยไรไอดำ",
        'งานกาก': "พูดดีๆหน่อยเธอ",
        'งานกระจอก': "ที่บ้านไม่เคร่งเรื่องมารยาทหรอ?"
    }

    response = responses.get(message.content.lower())
    if response:
        await message.channel.send(response)

# รันบอทด้วยโทเค็น
bot.run('YOUR_BOT_TOKEN')
