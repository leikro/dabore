
# -*- coding: utf-8 -*-

# Edited from script LineVodka script made by Merkremont

from LineAlpha import LineClient

from LineAlpha.LineApi import LineTracer

from LineAlpha.LineThrift.ttypes import Message

from LineAlpha.LineThrift.TalkService import Client

import time, datetime, random ,sys, re, string, os, json


reload(sys)

sys.setdefaultencoding('utf-8')


client = LineClient()

client._qrLogin("line://au/q/")


profile, setting, tracer = client.getProfile(), client.getSettings(), LineTracer(client)

offbot, messageReq, wordsArray, waitingAnswer = [], {}, {}, {}


print client._loginresult()


wait = {

    'readPoint':{},

    'readMember':{},

    'setTime':{},

    'ROM':{}

   }


setTime = {}

setTime = wait["setTime"]


def sendMessage(to, text, contentMetadata={}, contentType=0):

    mes = Message()

    mes.to, mes.from_ = to, profile.mid

    mes.text = text


    mes.contentType, mes.contentMetadata = contentType, contentMetadata

    if to not in messageReq:

        messageReq[to] = -1

    messageReq[to] += 1

    client._client.sendMessage(messageReq[to], mes)


def NOTIFIED_ADD_CONTACT(op):

    try:

        sendMessage(op.param1, client.getContact(op.param1).displayName + "Thanks for add")

    except Exception as e:

        print e

        print ("\n\nNOTIFIED_ADD_CONTACT\n\n")

        return


tracer.addOpInterrupt(5,NOTIFIED_ADD_CONTACT)


def NOTIFIED_ACCEPT_GROUP_INVITATION(op):

    #print op

    try:

        sendMessage(op.param1, client.getContact(op.param2).displayName + "WELCOME to " + group.name)

    except Exception as e:

        print e

        print ("\n\nNOTIFIED_ACCEPT_GROUP_INVITATION\n\n")

        return


tracer.addOpInterrupt(17,NOTIFIED_ACCEPT_GROUP_INVITATION)


def NOTIFIED_KICKOUT_FROM_GROUP(op):

    try:

        sendMessage(op.param1, client.getContact(op.param3).displayName + " Good Bye\n(*´･ω･*)")

    except Exception as e:

        print e

        print ("\n\nNOTIFIED_KICKOUT_FROM_GROUP\n\n")

        return


tracer.addOpInterrupt(19,NOTIFIED_KICKOUT_FROM_GROUP)


def NOTIFIED_LEAVE_GROUP(op):

    try:

        sendMessage(op.param1, client.getContact(op.param2).displayName + " Good Bye\n(*´･ω･*)")

    except Exception as e:

        print e

        print ("\n\nNOTIFIED_LEAVE_GROUP\n\n")

        return


tracer.addOpInterrupt(15,NOTIFIED_LEAVE_GROUP)


def NOTIFIED_READ_MESSAGE(op):

    #print op

    try:

        if op.param1 in wait['readPoint']:

            Name = client.getContact(op.param2).displayName

            if Name in wait['readMember'][op.param1]:

                pass

            else:

                wait['readMember'][op.param1] += "\n・" + Name

                wait['ROM'][op.param1][op.param2] = "・" + Name

        else:

            pass

    except:

        pass


tracer.addOpInterrupt(55, NOTIFIED_READ_MESSAGE)


def RECEIVE_MESSAGE(op):

    msg = op.message

    try:

        if msg.contentType == 0:

            try:

                if msg.to in wait['readPoint']:

                    if msg.from_ in wait["ROM"][msg.to]:

                        del wait["ROM"][msg.to][msg.from_]

                else:

                    pass

            except:

                pass

        else:

            pass

    except KeyboardInterrupt:

	 sys.exit(0)

    except Exception as error:

        print error

        print ("\n\nRECEIVE_MESSAGE\n\n")

        return


tracer.addOpInterrupt(26, RECEIVE_MESSAGE)


def SEND_MESSAGE(op):

    msg = op.message

    try:

        if msg.toType == 2:

            if msg.contentType == 0:

                #if "gname:" in msg.text:

#--------------------------------------------------------------

                if msg.text == "Mulai":

                    print "ok"

                    _name = msg.text.replace("Mulai","")

                    gs = client.getGroup(msg.to)

                    sendMessage(msg.to,"Kick By Leikro - Leikro/nsaya tidak bertanggung jawab apabila grup anda rata karena bot ini, silahkan kalian tanya sendiri akun ini\nTerimakasih")

                    targets = []

                    for g in gs.members:

                        if _name in g.displayName:

                            targets.append(g.mid)

                    if targets == []:

                        sendMessage(msg.to,"error")

                    else:

                        for target in targets:

                            try:

                                klist=[client]

                                kicker=random.choice(klist)

                                kicker.kickoutFromGroup(msg.to,[target])

                                print (msg.to,[g.mid])

                            except:

                                sendText(msg.to,"error")

#-------------------------------------------------------------			

		if msg.text == "Salken all":

                    start = time.time()

                    sendMessage(msg.to, "hehehe")

                    elapsed_time = time.time() - start

                    sendMessage(msg.to, "%sseconds" % (elapsed_time))

#-------------------------------------------------------------

                if msg.text == "Spam":

                    sendMessage(msg.to,"3")

                    sendMessage(msg.to,"2")

                    sendMessage(msg.to,"1")

                    sendMessage(msg.to,"Fuck You All")

                    sendMessage(msg.to,"I will kill you")

                    sendMessage(msg.to,"Let It Be")

                    sendMessage(msg.to,"Guns N' Rosess")

                    sendMessage(msg.to,"The Beatles")

                    sendMessage(msg.to,"Gapunya Kisah Kasih di sekolah haha")

                    sendMessage(msg.to,"Anti Galau Galau Club")

                    sendMessage(msg.to,"You Know me?")

                    sendMessage(msg.to,"Ku harus jujur, pada perasaanku")

                    sendMessage(msg.to,"Ku suka dirimu ku suka")

                    sendMessage(msg.to,"Ku berlari sekuat tenaga")

                    sendMessage(msg.to,"Dan Ku terjatuh ke sepitenk")

                    sendMessage(msg.to,"Ku teriak sebisa suaraku")

                    sendMessage(msg.to,"Ku suka makan")

                    sendMessage(msg.to,"yg ada gua makan gaada yaudah")

                    sendMessage(msg.to,"Tak akan ku sembunyikan")

                    sendMessage(msg.to,"Oooooo Rambo Rambe Rambo Aronawa Kombe")

                    sendMessage(msg.to,"Makan Gak Makan Kelaperan lah wkwj")

                    sendMessage(msg.to,"Hati ini pun resah tidak tertahankan")

                    sendMessage(msg.to,"Sekarang juga yang bisa ku lakukan")

                    sendMessage(msg.to,"Gak ada yang gak mungkin di dunia ini")

                    sendMessage(msg.to,"Mengapa sedari tadi")

                    sendMessage(msg.to,"Aku hanya menatap langit")

                    sendMessage(msg.to,"dan menatap bintang")

                    sendMessage(msg.to,"masih di sini")

                    sendMessage(msg.to,"masih dengan perasaan yang sama")

                    sendMessage(msg.to,"dengan orang yang sama")

                    sendMessage(msg.to,"Ku yakin ooo ku yakin")

                    sendMessage(msg.to,"kau akan mencret")

                    sendMessage(msg.to,"Ku yakin ooo ku yakin")

                    sendMessage(msg.to,"kau bau tai")

                    sendMessage(msg.to,"Ku yakin ooo ku yakin")

                    sendMessage(msg.to,"dirimu tak secantik korengmu")

                    sendMessage(msg.to,"Ku ingin kau mendengarkan")

                    sendMessage(msg.to,"Hey Rambo Rambe Rambo Aronawa Kombe")

                    sendMessage(msg.to,"Jika jika kamu ragu")

                    sendMessage(msg.to,"Takkan bisa memulai apapun")

                    sendMessage(msg.to,"silakan minum baygon")

                    sendMessage(msg.to,"Jujurlah dari sekarang juga")

                    sendMessage(msg.to,"Jika kau bersuar")

                    sendMessage(msg.to,"Cahaya kan bersinar")

                    sendMessage(msg.to,"kalo ada senter")

                    sendMessage(msg.to,"Ku berlari sekuat tenaga")

                    sendMessage(msg.to,"Ku suka selalu ku suka")

                    sendMessage(msg.to,"makan bakso")

                    sendMessage(msg.to,"Ku suka dirimu ku suka")

                    sendMessage(msg.to,"yang bau")

                    sendMessage(msg.to,"Ku suka selalu ku suka")

                    sendMessage(msg.to,"Ku teriakkan ditengah angin")

                    sendMessage(msg.to,"ditemani debu dan sampah nempel di muka")

                    sendMessage(msg.to,"Walau susah untuk ku bernapas")

                    sendMessage(msg.to,"itu tandanya sesak nafas")

                    sendMessage(msg.to,"Oooo rambo rambe rambo arobawa kombe")

                    sendMessage(msg.to,"Katakan dengan berani")

                    sendMessage(msg.to,"Jika kau diam kan tetap sama")

                    sendMessage(msg.to,"Janganlah kau merasa malu")

                    sendMessage(msg.to,"itu muka apa gorengan")

                    sendMessage(msg.to,"“ku suka tahu")

                    sendMessage(msg.to,"“ku suka tempe")

                    sendMessage(msg.to,"Ungkapkan perasaanmu")

                    sendMessage(msg.to,"Jujurlah dari sekarang juga..")

                    sendMessage(msg.to,"SPAM IS DONE")

                    sendMessage(msg.to,"Created By : Leikrus")

#-------------------------------------------------------------

                if msg.text == "Tagall":

		 group = client.getGroup(msg.to)

		 mem = [contact.mid for contact in group.members]

		 for mm in mem:

		 xname = client.getContact(mm).displayName

		 xlen = str(len(xname)+1)

		 msg.contentType = 0

                       msg.text = "@"+xname+" "

		 msg.contentMetadata ={'MENTION':'{"MENTIONEES":[{"S":"0","E":'+json.dumps(xlen)+',"M":'+json.dumps(mm)+'}]}','EMTVER':'4'}

		 try:

                         client.sendMessage(msg)

		 except Exception as error:

                   	 print error

#-------------------------------------------------------------

        else:

            pass


    except Exception as e:

        print e

        print ("\n\nSEND_MESSAGE\n\n")

        return


tracer.addOpInterrupt(25,SEND_MESSAGE)


while True:

    tracer.execute()
