import discord
import asyncio
import os

from discord.ext import commands

state = discord.Game("| .help |")  
#state 변수로 현재 상태를 나타냄 ("상태메세지")

bot = commands.Bot(command_prefix = '.', help_command = None, #help command on/off 
#     commands.Bot 으로 봇 객체 # command_prefix는 봇 명령어 접수사
                   status = discord.Status.online, activity = state) 
                 # status로 봇의 상태 # activity로 상태메시지를 설정
                 # online    offline    do_not_distrub    ilde 


@bot.event
async def on_ready():
    print(f'{bot.user.name,} connect')
    
@bot.command() 
#bot.command() 명령어 
async def ping(ctx): 
#async ,await는 비동기 함수 
    await ctx.send(f'ping = {round(round(bot.latency, 4)*1000)}ms') 
        # ctx = 매개변수로 넣어둬야 접수사가 읽고 명령을 실행 
        
@bot.command(name="참가", pass_context=True)
async def join(ctx):
    if ctx.author.voice and ctx.author.voice.channel: # 채널에 들어가 있는지 파악
        channel = ctx.author.voice.channel # 채널 구하기
        await channel.connect() # 채널 연결
    else: # 유저가 채널에 없으면
        await ctx.send("채널에 연결되지 않았습니다.")


@bot.command(aliases=['안녕','안녕하세요','하이','하이요','하이루','ㅎㅇ','ㅎㅇㅎㅇ','hi','gdgd','gd'])
async def hello(ctx):
    await ctx.send(f'{ctx.author.mention}님 안녕하세요! 환영합니다!')
                    # ctx.author.mention 멘션 = @               
    #await ctx.send("{}님 안녕하세요! 환영합니다!".format(ctx.author.mention)) 

@bot.command(
    aliases = [
        'h', '도움말', '명령어', '명령어 리스트', '도움말 리스트', '도움', '헬프', '설명서', '설명'])
           # aliases=[] 다른 명령어를 사용해도 인식하게 만드는 함수이다

async def help(ctx):
        # embed = 메세지를 정리하여 보여주는 기능

    embed = discord.Embed(
        title = "[명령어 리스트]", description="`Frist_Bot의 명령어 리스트 입니다.`", color = 0xF4F505)
  # title - 제목              description은 title 밑에 있는 설명

    embed.set_thumbnail(
        url = "https://cdn.discordapp.com/attachments/663745884315451405/968505951575502868/unknown.png")
        
  # embed.set_thumbnail = 썸네일 사진
    embed.set_image(
        url = "") 

  # embed.set_image = 큰 사진
    embed.add_field(
        name = "1 . 인사", value = "`[안녕]` `[안녕하세요]` `[ㅎㅇ]` `[ㅎㅇㅎㅇ]` `[hi]` `[gdgd]` `[gd]`", inline = True) 
                                                                                                       # inline = True
  # embed.add_field(name = '필드 이름', value='필드 값',                                                  inline=True 또는 False)
                  # name - 큰 글자      value - 작은글자                                                  inline - False - 세로 출력 inline - True - 가로 출력 
                                         
    embed.add_field(
        name = "2. 명령어", value = "`[명령어]` `[명령어 리스트]` `[도움말]` `[도움말 리스트]` `[도움]` `[설명]` `[설명]`", inline = False)                                                                            
    
    embed.add_field(
        name = "3. 음악재생",value = "`아직 모름`", inline = True)
    
    embed.add_field(
        name = "4. 아직모름", value = "`아직 모름`", inline = False)
    
    embed.set_footer(
  # embed.set_footer(text = '꼬릿말')
        text = "\"Future_Music_Bot\" made by 재얄",
        icon_url="https://cdn.discordapp.com/attachments/663745884315451405/968505712332374046/unknown.png")
    await ctx.send(embed = embed)
'''
@bot.command()
async def 따라하기(ctx,*,text):
    await ctx.send(text)
'''

bot.run('OTY4NDExMjg0ODAwNDEzNzE2.GRK-VT.efDDSpVCdi5puzEWUTA3SWU635dcGTay92TLSk') 
#bot run에 디스코드 토큰값을 넣어주면 디스코드에 봇이 활성화가 된다.

