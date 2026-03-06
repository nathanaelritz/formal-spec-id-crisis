--------------------------------------------------------------
Verification summary:

Query not event(LeakedAK(pubAK_5)) is false.

Query not event(LeakedEK(pubEK_7)) is false.

Query not event(Accepted(ev)) is false.

Query not event(Appraised(log)) is false.

Query not event(ClientConn(ev)) is false.

Query not event(ClientFinished(pubAK_5,psk_2,cr_2,sr_2,offer_2,mode_2,kc_4,ks_4,ems_4,rms_2)) is false.

Query not event(ClientFinRecentAgr(ID_S_4,ID_C_3,pubEK_7,psk_2,offer_2,mode_2,kc_4,ks_4,ems_4,rms_2,cr_2,sr_2)) is false.

Query not event(ServerFinished(cr_2,sr_2,psk_2,p,offer_2,mode_2,kc_4,ks_4,ems_4,rms_2)) is false.

Query not (event(ServerID(idS,gxy_2)) && event(ClientID(idXS,gxy_2))) is false.

Query not event(AcceptedRdata(rdata_1)) is false.

Query event(ServerFinished(cr_2,sr_2,psk_2,pubEK_7,offer_2,mode_2,kc_4,ks_4,ems_4,rms_2)) ==> event(ServerChoosesKEX(cr_2,sr_2,DHE_13(WeakDH,e))) || event(ServerChoosesHash(cr',sr',WeakHash)) || event(SentBadElement) || event(LeakedAK(pubAK_5)) || event(LeakedEK(pubEK_7)) is false.

Query attacker(privAK[!1 = v_68]) ==> event(LeakedAK(pk(privAK[!1 = v_69]))) is true.

Query attacker(privAK[!1 = v_68]) ==> event(LeakedAK(pubAK_5)) is true.

Query event(ClientFinished(pk(privAK[!1 = v_68]),psk_2,cr_2,sr_2,offer_2,mode_2,kc_4,ks_4,ems_4,rms_2)) && attacker(privAK[!1 = v_69]) ==> event(LeakedAK(pk(privAK[!1 = v_70]))) is true.

Query attacker(privEK[!2 = v_68,!1 = v_69]) ==> event(LeakedEK(pk(privEK[!2 = v_70,!1 = v_71]))) is true.

Query attacker(privEK[!2 = v_68,!1 = v_69]) ==> event(LeakedEK(pubEK_7)) is true.

Query event(ClientFinished(pk(privEK[!2 = v_68,!1 = v_69]),psk_2,cr_2,sr_2,offer_2,mode_2,kc_4,ks_4,ems_4,rms_2)) && attacker(privEK[!2 = v_70,!1 = v_71]) ==> event(LeakedEK(pk(privEK[!2 = v_72,!1 = v_73]))) is true.

Query event(ClientFinished(pubEK_7,psk_2,cr_2,sr_2,offer_2,mode_2,kc_4,ks_4,ems_4,rms_2)) && attacker(kc_4) ==> event(ServerChoosesKEX(cr_2,sr_2,DHE_13(WeakDH,e))) || event(ServerChoosesHash(cr',sr',WeakHash)) || event(SentBadElement) || event(LeakedAK(pubAK_5)) is true.

Query event(ClientFinished(pubEK_7,psk_2,cr_2,sr_2,offer_2,mode_2,kc_4,ks_4,ems_4,rms_2)) && attacker(kc_4) ==> event(ServerChoosesKEX(cr_2,sr_2,DHE_13(WeakDH,e))) || event(ServerChoosesHash(cr',sr',WeakHash)) || event(SentBadElement) || event(LeakedEK(pubEK_7)) is true.

Query event(ClientFinished(pubEK_7,psk_2,cr_2,sr_2,offer_2,mode_2,kc_4,ks_4,ems_4,rms_2)) && attacker(kc_4) ==> event(ServerChoosesKEX(cr_2,sr_2,DHE_13(WeakDH,e))) || event(ServerChoosesHash(cr',sr',WeakHash)) || event(SentBadElement) is false.

Query event(ClientFinished(pubEK_7,psk_2,cr_2,sr_2,offer_2,mode_2,kc_4,ks_4,ems_4,rms_2)) && attacker(kc_4) ==> event(ServerChoosesKEX(cr_2,sr_2,DHE_13(WeakDH,e))) || event(ServerChoosesHash(cr',sr',WeakHash)) || event(SentBadElement) || event(LeakedAK(anyAK)) || event(LeakedEK(pubEK_7)) is true.

Query event(ClientFinished(pubEK_7,psk_2,cr_2,sr_2,offer_2,mode_2,kc_4,ks_4,ems_4,rms_2)) && attacker(kc_4) ==> event(ServerChoosesKEX(cr_2,sr_2,DHE_13(WeakDH,e))) || event(ServerChoosesHash(cr',sr',WeakHash)) || event(SentBadElement) || event(LeakedAK(anyAK)) is true.

Query event(ClientFinished(pubEK_7,psk_2,cr_2,sr_2,offer_2,mode_2,kc_4,ks_4,ems_4,rms_2)) && attacker(kc_4) ==> event(ServerChoosesKEX(cr_2,sr_2,DHE_13(WeakDH,e))) || event(ServerChoosesHash(cr',sr',WeakHash)) || event(SentBadElement) || event(LeakedEK(pubEK_7)) is true.

Query event(ClientFinished(pubEK_7,psk_2,cr_2,sr_2,offer_2,mode_2,kc_4,ks_4,ems_4,rms_2)) && attacker(kc_4) ==> event(ServerChoosesKEX(cr_2,sr_2,DHE_13(WeakDH,e))) || event(ServerChoosesHash(cr',sr',WeakHash)) || event(SentBadElement) is false.

Query event(ClientComp(ID_S_4,pubEK_7,psk_2,offer_2,mode_2,kc_4,ks_4,ems_4,rms_2,cr_2,sr_2,pubEK_7,dev_state)) && attacker(kc_4) ==> event(ServerChoosesKEX(cr_2,sr_2,DHE_13(WeakDH,e))) || event(ServerChoosesHash(cr',sr',WeakHash)) || event(SentBadElement) || event(LeakedAK(pubAK_5)) is true.

Query event(ClientComp(ID_S_4,pubEK_7,psk_2,offer_2,mode_2,kc_4,ks_4,ems_4,rms_2,cr_2,sr_2,pubEK_7,dev_state)) && attacker(kc_4) ==> event(ServerChoosesKEX(cr_2,sr_2,DHE_13(WeakDH,e))) || event(ServerChoosesHash(cr',sr',WeakHash)) || event(SentBadElement) || event(LeakedEK(pubEK_7)) is true.

Query event(ClientComp(ID_S_4,pubEK_7,psk_2,offer_2,mode_2,kc_4,ks_4,ems_4,rms_2,cr_2,sr_2,pubEK_7,dev_state)) && attacker(kc_4) ==> event(ServerChoosesKEX(cr_2,sr_2,DHE_13(WeakDH,e))) || event(ServerChoosesHash(cr',sr',WeakHash)) || event(SentBadElement) is false.

Query event(ClientRA2(pubAK_5,pubEK_7,dev_state)) ==> event(ServerRA2(pubAK_5,pubEK_7,dev_state)) || event(LeakedAK(pubAK_5)) is true.

Query event(ClientRA2(pubAK_5,pubEK_7,dev_state)) ==> event(ServerRA2(pubAK_5,pubEK_7,dev_state)) || event(LeakedEK(pubEK_7)) is false.

Query event(ClientRA2(pubAK_5,pubEK_7,dev_state)) ==> event(ServerRA2(pubAK_5,pubEK_7,dev_state)) || event(LeakedAK(anyAK)) is true.

Query event(ClientRA3(pubAK_5,pubEK_7,dev_state,ID_C_3)) ==> event(ServerRA2(pubAK_5,pubEK_7,dev_state)) || event(LeakedAK(pubAK_5)) is true.

Query event(ClientRA3(pubAK_5,pubEK_7,dev_state,ID_C_3)) ==> event(ServerRA2(pubAK_5,pubEK_7,dev_state)) || event(LeakedEK(pubEK_7)) is false.

Query event(ClientRA(pubAK_5,pubEK_7,dev_state,ev)) ==> event(ServerRA(ID,pubEK_7,pubAK_5,pubEK_7,dev_state,ev)) || event(LeakedAK(pubAK_5)) is true.

Query event(ClientRA(pubAK_5,pubEK_7,dev_state,ev)) ==> event(ServerRA(ID,pubEK_7,pubAK_5,pubEK_7,dev_state,ev)) || event(LeakedEK(pubEK_7)) is false.

Query event(ClientRANew(NULL_ID,NULL_pubkey,pubAK_5,pubEK_7,dev_state,ev)) ==> event(ServerRA(ID,pubEK_7,pubAK_5,pubEK_7,dev_state,ev)) || event(LeakedAK(pubAK_5)) is true.

Query event(ClientRA(pubAK_5,pubEK_7,dev_state,ev)) ==> event(ServerRA(ID,pubEK_7,pubAK_5,pubEK_7,dev_state,ev)) is false.

Query event(ClientRA(pubAK_5,pubEK_7,dev_state,ev)) ==> event(ServerRA(ID,pubEK_7,pubAK_5,pubEK_7,dev_state,ev)) || event(LeakedAK2(ID,pubEK_7,pubAK_5)) is false.

Query event(ClientRAWithoutAK(pubEK_7,dev_state,ev)) ==> event(ServerRAWithoutAK(pubEK_7,dev_state,ev)) || event(LeakedAK(pubAK_5)) is true.

Query event(ClientRAWithoutAK(pubEK_7,dev_state,ev)) ==> event(ServerRAWithoutAK(pubEK_7,dev_state,ev)) || event(LeakedEK(pubEK_7)) is false.

Query inj-event(ClientRA2(pubAK_5,pubEK_7,dev_state)) ==> inj-event(ServerRA2(pubAK_5,pubEK_7,dev_state)) || event(LeakedAK(pubAK_5)) is true.

Query inj-event(ClientRA2(pubAK_5,pubEK_7,dev_state)) ==> inj-event(ServerRA2(pubAK_5,pubEK_7,dev_state)) || event(LeakedEK(pubEK_7)) is false.

Query inj-event(ClientRA2(pubAK_5,pubEK_7,dev_state)) ==> inj-event(ServerRA2(pubAK_5,pubEK_7,dev_state)) || event(LeakedAK(pubAK_5)) || event(ServerChoosesKEX(cr_2,sr_2,DHE_13(WeakDH,e))) || event(ServerChoosesHash(cr_2,sr_2,WeakHash)) is true.

Query inj-event(ClientRA2(pubAK_5,pubEK_7,dev_state)) ==> inj-event(ServerRA2(pubAK_5,pubEK_7,dev_state)) || event(LeakedEK(pubEK_7)) || event(ServerChoosesKEX(cr_2,sr_2,DHE_13(WeakDH,e))) || event(ServerChoosesHash(cr_2,sr_2,WeakHash)) is true.

Query inj-event(ClientRA(pubAK_5,pubEK_7,dev_state,ev)) ==> inj-event(ServerRA(ID,pubEK_7,pubAK_5,pubEK_7,dev_state,ev)) || event(LeakedAK(pubAK_5)) is true.

Query inj-event(ClientRA(pubAK_5,pubEK_7,dev_state,ev)) ==> inj-event(ServerRA(ID,pubEK_7,pubAK_5,pubEK_7,dev_state,ev)) || event(LeakedEK(pubEK_7)) is false.

Query inj-event(ClientRA(pubAK_5,pubEK_7,dev_state,ev)) ==> inj-event(ServerRA(ID,pubEK_7,pubAK_5,pubEK_7,dev_state,ev)) || event(LeakedAK(pubAK_5)) || event(ServerChoosesKEX(cr_2,sr_2,DHE_13(WeakDH,e))) || event(ServerChoosesHash(cr_2,sr_2,WeakHash)) is true.

Query inj-event(ClientRA(pubAK_5,pubEK_7,dev_state,ev)) ==> inj-event(ServerRA(ID,pubEK_7,pubAK_5,pubEK_7,dev_state,ev)) || event(LeakedEK(pubEK_7)) || event(ServerChoosesKEX(cr_2,sr_2,DHE_13(WeakDH,e))) || event(ServerChoosesHash(cr_2,sr_2,WeakHash)) is true.

Query inj-event(Accepted(ev)) ==> inj-event(Sent(ev)) || event(LeakedAK(pubAK_5)) || event(ServerChoosesKEX(cr_2,sr_2,DHE_13(WeakDH,e))) || event(ServerChoosesHash(cr_2,sr_2,WeakHash)) is true.

Query inj-event(Accepted(ev)) ==> inj-event(Sent(ev)) || event(LeakedEK(pubEK_7)) || event(ServerChoosesKEX(cr_2,sr_2,DHE_13(WeakDH,e))) || event(ServerChoosesHash(cr_2,sr_2,WeakHash)) is true.

Query inj-event(Accepted(ev)) ==> inj-event(Sent(ev)) || event(ServerChoosesKEX(cr_2,sr_2,DHE_13(WeakDH,e))) || event(ServerChoosesHash(cr_2,sr_2,WeakHash)) is false.

Query inj-event(AcceptedWithPubEK(ev,pubEK_7)) ==> inj-event(Sent(ev)) || event(LeakedEK(pubEK_7)) || event(ServerChoosesKEX(cr_2,sr_2,DHE_13(WeakDH,e))) || event(ServerChoosesHash(cr_2,sr_2,WeakHash)) is true.

Query inj-event(AcceptedWithPubEK(ev,pubEK_7)) ==> inj-event(Sent(ev)) || event(LeakedAK(pubAK_5)) || event(ServerChoosesKEX(cr_2,sr_2,DHE_13(WeakDH,e))) || event(ServerChoosesHash(cr_2,sr_2,WeakHash)) is true.

Query inj-event(AcceptedWithPubEK(ev,pubEK_7)) ==> inj-event(Sent(ev)) || event(ServerChoosesKEX(cr_2,sr_2,DHE_13(WeakDH,e))) || event(ServerChoosesHash(cr_2,sr_2,WeakHash)) is false.

Query inj-event(AcceptedWithPubEK(ev,pubEK_7)) ==> inj-event(SentWithPubEK(ev,pubEK_7)) || event(LeakedEK(pubEK_7)) || event(ServerChoosesKEX(cr_2,sr_2,DHE_13(WeakDH,e))) || event(ServerChoosesHash(cr_2,sr_2,WeakHash)) is true.

Query inj-event(AcceptedWithPubEK(ev,pubEK_7)) ==> inj-event(SentWithPubEK(ev,pubEK_7)) || event(LeakedAK(pubAK_5)) || event(ServerChoosesKEX(cr_2,sr_2,DHE_13(WeakDH,e))) || event(ServerChoosesHash(cr_2,sr_2,WeakHash)) is true.

Query inj-event(AcceptedWithPubEK(ev,pubEK_7)) ==> inj-event(SentWithPubEK(ev,pubEK_7)) || event(ServerChoosesKEX(cr_2,sr_2,DHE_13(WeakDH,e))) || event(ServerChoosesHash(cr_2,sr_2,WeakHash)) is false.

Query inj-event(AcceptedRdata(dev_state)) ==> inj-event(SentRdata(dev_state)) || event(LeakedEK(pubEK_7)) || event(ServerChoosesKEX(cr_2,sr_2,DHE_13(WeakDH,e))) || event(ServerChoosesHash(cr_2,sr_2,WeakHash)) is true.

Query inj-event(AcceptedRdata(dev_state)) ==> inj-event(SentRdata(dev_state)) || event(LeakedAK(pubAK_5)) || event(ServerChoosesKEX(cr_2,sr_2,DHE_13(WeakDH,e))) || event(ServerChoosesHash(cr_2,sr_2,WeakHash)) is true.

Query inj-event(AcceptedRdata(dev_state)) ==> inj-event(SentRdata(dev_state)) || event(ServerChoosesKEX(cr_2,sr_2,DHE_13(WeakDH,e))) || event(ServerChoosesHash(cr_2,sr_2,WeakHash)) is false.

Query inj-event(ClientConn(ev)) ==> inj-event(Sent(ev)) || event(LeakedAK(pubAK_5)) || event(ServerChoosesKEX(cr_2,sr_2,DHE_13(WeakDH,e))) || event(ServerChoosesHash(cr_2,sr_2,WeakHash)) is true.

Query inj-event(ClientConn(ev)) ==> inj-event(Sent(ev)) || event(LeakedEK(pubEK_7)) || event(ServerChoosesKEX(cr_2,sr_2,DHE_13(WeakDH,e))) || event(ServerChoosesHash(cr_2,sr_2,WeakHash)) is true.

Query inj-event(ClientConn(ev)) ==> inj-event(Sent(ev)) || event(ServerChoosesKEX(cr_2,sr_2,DHE_13(WeakDH,e))) || event(ServerChoosesHash(cr_2,sr_2,WeakHash)) is false.

Query event(ServerID(idS,gxy_2)) && event(ClientID(idXS,gxy_2)) ==> idS = idXS || event(ServerChoosesKEX(cr_2,sr_2,DHE_13(WeakDH,e))) || event(ServerChoosesHash(cr',sr',WeakHash)) || event(SentBadElement) || event(LeakedEK(pubEK_7)) is true.

Query event(ServerID(idS,gxy_2)) && event(ClientID(idXS,gxy_2)) ==> idS = idXS || event(ServerChoosesKEX(cr_2,sr_2,DHE_13(WeakDH,e))) || event(ServerChoosesHash(cr',sr',WeakHash)) || event(SentBadElement) || event(LeakedAK(pubAK_5)) is true.

Query event(ServerID(idS,gxy_2)) && event(ClientID(idXS,gxy_2)) ==> idS = idXS || event(ServerChoosesKEX(cr_2,sr_2,DHE_13(WeakDH,e))) || event(ServerChoosesHash(cr',sr',WeakHash)) || event(SentBadElement) is true.

Query event(ClientFinishedAliveness(ID_S_4)) ==> event(PreServerFinishedAliveness(ID_S_4)) || event(ServerChoosesKEX(cr_2,sr_2,DHE_13(WeakDH,e))) || event(ServerChoosesHash(cr',sr',WeakHash)) || event(SentBadElement) || event(LeakedEK(pubEK_7)) is true.

Query event(ClientFinishedAliveness(ID_S_4)) ==> event(PreServerFinishedAliveness(ID_S_4)) || event(ServerChoosesKEX(cr_2,sr_2,DHE_13(WeakDH,e))) || event(ServerChoosesHash(cr',sr',WeakHash)) || event(SentBadElement) || event(LeakedAK(pubAK_5)) is true.

Query event(ClientFinishedAliveness(ID_S_4)) ==> event(PreServerFinishedAliveness(ID_S_4)) || event(ServerChoosesKEX(cr_2,sr_2,DHE_13(WeakDH,e))) || event(ServerChoosesHash(cr',sr',WeakHash)) || event(SentBadElement) is false.

Query event(ClientFin1WayAgr(ID_S_4,pubEK_7,psk_2,offer_2,mode_2,kc_4,ks_4,ems_4,rms_2)) ==> event(PreServerFin1WayAgr(ID_S_4,pubEK_7,psk_2,offer_2,mode_2,kc_4,ks_4,ems_4)) || event(ServerChoosesKEX(cr_2,sr_2,DHE_13(WeakDH,e))) || event(ServerChoosesHash(cr',sr',WeakHash)) || event(SentBadElement) || event(LeakedAK(pubAK_5)) is true.

Query event(ClientFin1WayAgr(ID_S_4,pubEK_7,psk_2,offer_2,mode_2,kc_4,ks_4,ems_4,rms_2)) ==> event(PreServerFin1WayAgr(ID_S_4,pubEK_7,psk_2,offer_2,mode_2,kc_4,ks_4,ems_4)) || event(ServerChoosesKEX(cr_2,sr_2,DHE_13(WeakDH,e))) || event(ServerChoosesHash(cr',sr',WeakHash)) || event(SentBadElement) || event(LeakedEK(pubEK_7)) is true.

Query event(ClientFin1WayAgr(ID_S_4,pubEK_7,psk_2,offer_2,mode_2,kc_4,ks_4,ems_4,rms_2)) ==> event(PreServerFin1WayAgr(ID_S_4,pubEK_7,psk_2,offer_2,mode_2,kc_4,ks_4,ems_4)) || event(ServerChoosesKEX(cr_2,sr_2,DHE_13(WeakDH,e))) || event(ServerChoosesHash(cr',sr',WeakHash)) || event(SentBadElement) is false.

Query inj-event(ClientFin1WayAgr(ID_S_4,pubEK_7,psk_2,offer_2,mode_2,kc_4,ks_4,ems_4,rms_2)) ==> inj-event(PreServerFin1WayAgr(ID_S_4,pubEK_7,psk_2,offer_2,mode_2,kc_4,ks_4,ems_4)) || event(ServerChoosesKEX(cr_2,sr_2,DHE_13(WeakDH,e))) || event(ServerChoosesHash(cr',sr',WeakHash)) || event(SentBadElement) || event(LeakedAK(pubAK_5)) || event(LeakedEK(pubEK_7)) is true.

Query inj-event(ClientFin1WayAgr(ID_S_4,pubEK_7,psk_2,offer_2,mode_2,kc_4,ks_4,ems_4,rms_2)) ==> inj-event(PreServerFin1WayAgr(ID_S_4,pubEK_7,psk_2,offer_2,mode_2,kc_4,ks_4,ems_4)) || event(ServerChoosesKEX(cr_2,sr_2,DHE_13(WeakDH,e))) || event(ServerChoosesHash(cr',sr',WeakHash)) || event(SentBadElement) || event(LeakedAK(pubAK_5)) || event(LeakedEK(pubEK_7)) is true.

Query inj-event(ClientFin1WayAgr(ID_S_4,pubEK_7,psk_2,offer_2,mode_2,kc_4,ks_4,ems_4,rms_2)) ==> inj-event(PreServerFin1WayAgr(ID_S_4,pubEK_7,psk_2,offer_2,mode_2,kc_4,ks_4,ems_4)) || event(ServerChoosesKEX(cr_2,sr_2,DHE_13(WeakDH,e))) || event(ServerChoosesHash(cr',sr',WeakHash)) || event(SentBadElement) is false.

Query inj-event(ClientFinRecent1WayAgr(ID_S_4,pubEK_7,psk_2,offer_2,mode_2,kc_4,ks_4,ems_4,rms_2,cr_2,sr_2)) ==> inj-event(PreServerFinRecent1WayAgr(ID_S_4,pubEK_7,psk_2,offer_2,mode_2,kc_4,ks_4,ems_4,cr_2,sr_2)) || event(ServerChoosesKEX(cr_2,sr_2,DHE_13(WeakDH,e))) || event(ServerChoosesHash(cr',sr',WeakHash)) || event(SentBadElement) || event(LeakedEK(pubEK_7)) is true.

Query inj-event(ClientFinRecent1WayAgr(ID_S_4,pubEK_7,psk_2,offer_2,mode_2,kc_4,ks_4,ems_4,rms_2,cr_2,sr_2)) ==> inj-event(PreServerFinRecent1WayAgr(ID_S_4,pubEK_7,psk_2,offer_2,mode_2,kc_4,ks_4,ems_4,cr_2,sr_2)) || event(ServerChoosesKEX(cr_2,sr_2,DHE_13(WeakDH,e))) || event(ServerChoosesHash(cr',sr',WeakHash)) || event(SentBadElement) || event(LeakedAK(pubAK_5)) is true.

Query inj-event(ClientFinRecent1WayAgr(ID_S_4,pubEK_7,psk_2,offer_2,mode_2,kc_4,ks_4,ems_4,rms_2,cr_2,sr_2)) ==> inj-event(PreServerFinRecent1WayAgr(ID_S_4,pubEK_7,psk_2,offer_2,mode_2,kc_4,ks_4,ems_4,cr_2,sr_2)) || event(ServerChoosesKEX(cr_2,sr_2,DHE_13(WeakDH,e))) || event(ServerChoosesHash(cr',sr',WeakHash)) || event(SentBadElement) is false.

Query inj-event(ClientFinRecent1WayAgr(ID_S_4,pubEK_7,psk_2,offer_2,mode_2,kc_4,ks_4,ems_4,rms_2,cr_2,sr_2)) ==> inj-event(PreServerFinRecent1WayAgr(ID_S_4,pubEK_7,psk_2,offer_2,mode_2,kc_4,ks_4,ems_4,cr_2,sr_2)) || event(ServerChoosesKEX(cr_2,sr_2,DHE_13(WeakDH,e))) || event(ServerChoosesHash(cr',sr',WeakHash)) || event(SentBadElement) || event(LeakedAK(pubAK_5)) is true.

Query inj-event(ClientFinRecent1WayAgr(ID_S_4,pubEK_7,psk_2,offer_2,mode_2,kc_4,ks_4,ems_4,rms_2,cr_2,sr_2)) ==> inj-event(PreServerFinRecent1WayAgr(ID_S_4,pubEK_7,psk_2,offer_2,mode_2,kc_4,ks_4,ems_4,cr_2,sr_2)) || event(ServerChoosesKEX(cr_2,sr_2,DHE_13(WeakDH,e))) || event(ServerChoosesHash(cr',sr',WeakHash)) || event(SentBadElement) || event(LeakedEK(pubEK_7)) is true.

Query inj-event(ClientFinRecent1WayAgr(ID_S_4,pubEK_7,psk_2,offer_2,mode_2,kc_4,ks_4,ems_4,rms_2,cr_2,sr_2)) ==> inj-event(PreServerFinRecent1WayAgr(ID_S_4,pubEK_7,psk_2,offer_2,mode_2,kc_4,ks_4,ems_4,cr_2,sr_2)) || event(ServerChoosesKEX(cr_2,sr_2,DHE_13(WeakDH,e))) || event(ServerChoosesHash(cr',sr',WeakHash)) || event(SentBadElement) is false.

Query inj-event(ClientFinished(pubEK_7,psk_2,cr_2,sr_2,offer_2,mode_2,kc_4,ks_4,ems_4,rms_2)) ==> inj-event(PreServerFinished(pubEK_7,psk_2,cr_2,sr_2,offer_2,mode_2,kc_4,ks_4,ems_4)) || event(ServerChoosesKEX(cr_2,sr_2,DHE_13(WeakDH,e))) || event(ServerChoosesHash(cr',sr',WeakHash)) || event(SentBadElement) || event(LeakedAK(pubAK_5)) is true.

Query inj-event(ClientFinished(pubEK_7,psk_2,cr_2,sr_2,offer_2,mode_2,kc_4,ks_4,ems_4,rms_2)) ==> inj-event(PreServerFinished(pubEK_7,psk_2,cr_2,sr_2,offer_2,mode_2,kc_4,ks_4,ems_4)) || event(ServerChoosesKEX(cr_2,sr_2,DHE_13(WeakDH,e))) || event(ServerChoosesHash(cr',sr',WeakHash)) || event(SentBadElement) || event(LeakedEK(pubEK_7)) is true.

Query inj-event(ClientFinishedWithID(ID,pubEK_7,pubAK_5,psk_2,cr_2,sr_2,offer_2,mode_2,kc_4,ks_4,ems_4,rms_2)) ==> inj-event(PreServerFinishedWithID(ID,pubEK_7,pubAK_5,psk_2,cr_2,sr_2,offer_2,mode_2,kc_4,ks_4,ems_4)) || event(ServerChoosesKEX(cr_2,sr_2,DHE_13(WeakDH,e))) || event(ServerChoosesHash(cr',sr',WeakHash)) || event(SentBadElement) || event(LeakedAK(pubAK_5)) is true.

Query inj-event(ClientFinishedWithID(ID,pubEK_7,pubAK_5,psk_2,cr_2,sr_2,offer_2,mode_2,kc_4,ks_4,ems_4,rms_2)) ==> inj-event(PreServerFinishedWithID(ID,pubEK_7,pubAK_5,psk_2,cr_2,sr_2,offer_2,mode_2,kc_4,ks_4,ems_4)) || event(ServerChoosesKEX(cr_2,sr_2,DHE_13(WeakDH,e))) || event(ServerChoosesHash(cr',sr',WeakHash)) || event(SentBadElement) || event(LeakedEK(pubEK_7)) is true.

Query inj-event(ClientFinishedWithID(ID,pubEK_7,pubAK_5,psk_2,cr_2,sr_2,offer_2,mode_2,kc_4,ks_4,ems_4,rms_2)) ==> inj-event(PreServerFinishedWithID(ID,pubEK_7,pubAK_5,psk_2,cr_2,sr_2,offer_2,mode_2,kc_4,ks_4,ems_4)) || event(ServerChoosesKEX(cr_2,sr_2,DHE_13(WeakDH,e))) || event(ServerChoosesHash(cr',sr',WeakHash)) || event(SentBadElement) is false.

Query inj-event(ClientComp(ID_S_4,pubEK_7,psk_2,offer_2,mode_2,kc_4,ks_4,ems_4,rms_2,cr_2,sr_2,pubEK_7,dev_state)) ==> inj-event(PreServerComp(ID_S_4,pubEK_7,psk_2,offer_2,mode_2,kc_4,ks_4,ems_4,cr_2,sr_2,pubEK_7,dev_state)) || event(ServerChoosesKEX(cr_2,sr_2,DHE_13(WeakDH,e))) || event(ServerChoosesHash(cr',sr',WeakHash)) || event(LeakedEK(pubEK_7)) is true.

Query inj-event(ClientComp(ID_S_4,pubEK_7,psk_2,offer_2,mode_2,kc_4,ks_4,ems_4,rms_2,cr_2,sr_2,pubEK_7,dev_state)) ==> inj-event(PreServerComp(ID_S_4,pubEK_7,psk_2,offer_2,mode_2,kc_4,ks_4,ems_4,cr_2,sr_2,pubEK_7,dev_state)) || event(ServerChoosesKEX(cr_2,sr_2,DHE_13(WeakDH,e))) || event(ServerChoosesHash(cr',sr',WeakHash)) || event(LeakedAK(pubAK_5)) is true.

Query inj-event(ClientComp(ID_S_4,pubEK_7,psk_2,offer_2,mode_2,kc_4,ks_4,ems_4,rms_2,cr_2,sr_2,pubEK_7,dev_state)) ==> inj-event(PreServerComp(ID_S_4,pubEK_7,psk_2,offer_2,mode_2,kc_4,ks_4,ems_4,cr_2,sr_2,pubEK_7,dev_state)) || event(ServerChoosesKEX(cr_2,sr_2,DHE_13(WeakDH,e))) || event(ServerChoosesHash(cr',sr',WeakHash)) is false.

--------------------------------------------------------------
