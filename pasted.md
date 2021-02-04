# 某pasted js的详细分析 附源码

今天收到了一位网友发来的js，说是c+v的，让我看看并公开了

打开一看 啊，果不其然 一眼扫去基本上80%都是paste，paste以外的部分写的像狗屎 性能优化极差 加载一下op都卡了。

那么下面是源码

## 源码

[下载](pasted.js)

## paste部分分析

菜单paste的部分我就不说了，毕竟功能最重要

- 123-186 屏幕中间环形aa指示器 来自他人的付费混淆js，改都不改直接copy and paste

  ```javascript
  Render['Arc'] = function (_0xbdacx4, _0xbdacx5, _0xbdacxb, _0xbdacxc, _0xbdacxd, _0xbdacxe, _0xbdacxf, _0xbdacx10) {
      _0xbdacxf = 360 / _0xbdacxf;
      for (var _0xbdacx2 = _0xbdacxd; _0xbdacx2 < _0xbdacxd + _0xbdacxe; _0xbdacx2 = _0xbdacx2 + _0xbdacxf) {
          var _0xbdacx11 = _0xbdacx2 * Math['PI'] / 180;
          var _0xbdacx12 = (_0xbdacx2 + _0xbdacxf) * Math['PI'] / 180;
          var _0xbdacx13 = Math['cos'](_0xbdacx11);
          var _0xbdacx14 = Math['sin'](_0xbdacx11);
          var _0xbdacx15 = Math['cos'](_0xbdacx12);
          var _0xbdacx16 = Math['sin'](_0xbdacx12);
          var _0xbdacx17 = _0xbdacx4 + _0xbdacx13 * _0xbdacxc;
          var _0xbdacx18 = _0xbdacx5 + _0xbdacx14 * _0xbdacxc;
          var _0xbdacx19 = _0xbdacx4 + _0xbdacx13 * _0xbdacxb;
          var _0xbdacx1a = _0xbdacx5 + _0xbdacx14 * _0xbdacxb;
          var _0xbdacx1b = _0xbdacx4 + _0xbdacx15 * _0xbdacxc;
          var _0xbdacx1c = _0xbdacx5 + _0xbdacx16 * _0xbdacxc;
          var _0xbdacx1d = _0xbdacx4 + _0xbdacx15 * _0xbdacxb;
          var _0xbdacx1e = _0xbdacx5 + _0xbdacx16 * _0xbdacxb;
          Render.Polygon([
              [_0xbdacx19, _0xbdacx1a],
              [_0xbdacx1d, _0xbdacx1e],
              [_0xbdacx17, _0xbdacx18]
          ], _0xbdacx10);
          Render.Polygon([
              [_0xbdacx17, _0xbdacx18],
              [_0xbdacx1d, _0xbdacx1e],
              [_0xbdacx1b, _0xbdacx1c]
          ], _0xbdacx10)
      }
  };
  const Renderer = {
      length: 0,
  };
  Renderer['Desync'] = function () {
      var screen_size = Render.GetScreenSize();
      const _0xbdacx4 = screen_size[0],
          _0xbdacx5 = screen_size[1];
      const _0xbdacx2f = UI.GetValue(['Rage', 'Anti Aim', 'General', 'Key assignment', 'AA Direction inverter']);
      const _0xbdacx30 = Local.GetViewAngles()[1] - Local.GetRealYaw();
      const me = Entity.GetLocalPlayer();
      const scoped = Entity.GetProp(me, "CCSPlayer", "m_bIsScoped")
  
      if (!scoped && Entity.IsAlive(me)) {
          for (var _0xbdacx2 = 0; _0xbdacx2 < 6.5; _0xbdacx2++) {
              Render.Circle(_0xbdacx4 / 2, _0xbdacx5 / 2, 5 + _0xbdacx2, [10, 10, 10, 140])
          };
          if (_0xbdacx2f == 1) {
              Render.Arc(_0xbdacx4 / 2, _0xbdacx5 / 2, 10, 5, 270, 180, 18, color_fake)
          } else {
              Render.Arc(_0xbdacx4 / 2, _0xbdacx5 / 2, 10, 5, 90, 180, 18, color_fake)
          }
          Render.Arc(_0xbdacx4 / 2, _0xbdacx5 / 2, 20, 16, _0xbdacx30 - 135, 45, 24, [color_fake[0], color_fake[1], color_fake[2], 200])
      }
      if (scoped && Entity.IsAlive(me)) {
          for (var _0xbdacx2 = 0; _0xbdacx2 < 6.5; _0xbdacx2++) {
              Render.Circle(_0xbdacx4 / 2, _0xbdacx5 / 2, 5 + _0xbdacx2, [10, 10, 10, 60])
          };
          if (_0xbdacx2f == 1) {
              Render.Arc(_0xbdacx4 / 2, _0xbdacx5 / 2, 10, 6, 270, 180, 18, [color_fake[0], color_fake[1], color_fake[2], 120])
          } else {
              Render.Arc(_0xbdacx4 / 2, _0xbdacx5 / 2, 10, 6, 90, 180, 18, [color_fake[0], color_fake[1], color_fake[2], 120])
          }
          Render.Arc(_0xbdacx4 / 2, _0xbdacx5 / 2, 20, 16, _0xbdacx30 - 135, 45, 24, [color_fake[0], color_fake[1], color_fake[2], 120])
      }
  };
  ```

- 367-410 AA左右指示器 paste自老版本dhdj.js 我寻思这玩意字体都可以实现，为啥非得从别人的js里paste

  ```javascript
  function AA_indicator() {
      var realBorderColor = [200, 200, 255, 160]
      var fakeBorderColor = [131, 67, 192, 200]
      var screen_size = Global.GetScreenSize();
      if (!UI.GetValue(["Rage", "Anti Aim", "General", "Key assignment", "AA Direction inverter"])) {
          Render.Line(screen_size[0] / 2 + 102, screen_size[1] / 2, screen_size[0] / 2 + 75, screen_size[1] / 2 + 16, realBorderColor);
          Render.Line(screen_size[0] / 2 + 102, screen_size[1] / 2, screen_size[0] / 2 + 75, screen_size[1] / 2 - 16, realBorderColor);
          Render.Line(screen_size[0] / 2 + 80, screen_size[1] / 2, screen_size[0] / 2 + 75, screen_size[1] / 2 + 16, realBorderColor);
          Render.Line(screen_size[0] / 2 + 80, screen_size[1] / 2, screen_size[0] / 2 + 75, screen_size[1] / 2 - 16, realBorderColor);
          Render.Line(screen_size[0] / 2 - 102, screen_size[1] / 2, screen_size[0] / 2 - 75, screen_size[1] / 2 + 16, fakeBorderColor);
          Render.Line(screen_size[0] / 2 - 102, screen_size[1] / 2, screen_size[0] / 2 - 75, screen_size[1] / 2 - 16, fakeBorderColor);
          Render.Line(screen_size[0] / 2 - 80, screen_size[1] / 2, screen_size[0] / 2 - 75, screen_size[1] / 2 + 16, fakeBorderColor);
          Render.Line(screen_size[0] / 2 - 80, screen_size[1] / 2, screen_size[0] / 2 - 75, screen_size[1] / 2 - 16, fakeBorderColor);
          Render.Polygon([
              [screen_size[0] / 2 + 75, screen_size[1] / 2 + 16],
              [screen_size[0] / 2 + 80, screen_size[1] / 2],
              [screen_size[0] / 2 + 102, screen_size[1] / 2]
          ], realBorderColor);
          Render.Polygon([
              [screen_size[0] / 2 - 102, screen_size[1] / 2],
              [screen_size[0] / 2 - 80, screen_size[1] / 2],
              [screen_size[0] / 2 - 75, screen_size[1] / 2 + 16]
          ], fakeBorderColor);
      } else {
          Render.Line(screen_size[0] / 2 + 102, screen_size[1] / 2, screen_size[0] / 2 + 75, screen_size[1] / 2 + 16, fakeBorderColor);
          Render.Line(screen_size[0] / 2 + 102, screen_size[1] / 2, screen_size[0] / 2 + 75, screen_size[1] / 2 - 16, fakeBorderColor);
          Render.Line(screen_size[0] / 2 + 80, screen_size[1] / 2, screen_size[0] / 2 + 75, screen_size[1] / 2 + 16, fakeBorderColor);
          Render.Line(screen_size[0] / 2 + 80, screen_size[1] / 2, screen_size[0] / 2 + 75, screen_size[1] / 2 - 16, fakeBorderColor);
          Render.Line(screen_size[0] / 2 - 102, screen_size[1] / 2, screen_size[0] / 2 - 75, screen_size[1] / 2 + 16, realBorderColor);
          Render.Line(screen_size[0] / 2 - 102, screen_size[1] / 2, screen_size[0] / 2 - 75, screen_size[1] / 2 - 16, realBorderColor);
          Render.Line(screen_size[0] / 2 - 80, screen_size[1] / 2, screen_size[0] / 2 - 75, screen_size[1] / 2 + 16, realBorderColor);
          Render.Line(screen_size[0] / 2 - 80, screen_size[1] / 2, screen_size[0] / 2 - 75, screen_size[1] / 2 - 16, realBorderColor);
          Render.Polygon([
              [screen_size[0] / 2 + 75, screen_size[1] / 2 + 16],
              [screen_size[0] / 2 + 80, screen_size[1] / 2],
              [screen_size[0] / 2 + 102, screen_size[1] / 2]
          ], fakeBorderColor);
          Render.Polygon([
              [screen_size[0] / 2 - 102, screen_size[1] / 2],
              [screen_size[0] / 2 - 80, screen_size[1] / 2],
              [screen_size[0] / 2 - 75, screen_size[1] / 2 + 
               16]
          ], realBorderColor);
      }
  }
  ```

- 413-438 菜单彩虹边框/背景 pasted自老版本dhdj.js 这玩意都不能自己写是得有多废物啊

  ```javascript
  function drawMenuBorder() {
      var screen_size = Global.GetScreenSize();
      var mp = UI.GetMenuPosition();
      var colors = HSV2RGB(Global.Realtime() * 0.5, 1, 1);
      Render.FilledRect(0, 0, screen_size[0], screen_size[1], [0, 0, 0, 100]);
      Render.GradientRect(mp[0] - 5, mp[1], 20, mp[3], 0, [colors.r, colors.g, colors.b, 255], [colors.b, colors.g, colors.r, 255]);
      Render.GradientRect(mp[0] - 5, mp[1] - 5, mp[2] + 10, 20, 1, [colors.r, colors.g, colors.b, 255], [colors.b, colors.g, colors.r, 255]);
      Render.GradientRect(mp[0] - 15 + mp[2], mp[1], 20, mp[3], 0, [colors.b, colors.g, colors.r, 255], [colors.r, colors.g, colors.b, 255]);
      Render.GradientRect(mp[0] - 5, mp[1] - 15 + mp[3], mp[2] + 10, 20, 1, [colors.b, colors.g, colors.r, 255], [colors.r, colors.g, colors.b, 255]);
  
      Render.GradientRect(mp[0] - 6, mp[1] - 4, 1, mp[3] + 8, 0, [colors.r, colors.g, colors.b, 255], [colors.b, colors.g, colors.r, 255]);
      Render.GradientRect(mp[0] - 7, mp[1] - 2, 1, mp[3] + 4, 0, [colors.r, colors.g, colors.b, 255], [colors.b, colors.g, colors.r, 255]);
      Render.GradientRect(mp[0] - 8, mp[1], 1, mp[3], 0, [colors.r, colors.g, colors.b, 255], [colors.b, colors.g, colors.r, 255]);
  
      Render.GradientRect(mp[0] + mp[2] + 5, mp[1] - 4, 1, mp[3] + 8, 0, [colors.b, colors.g, colors.r, 255], [colors.r, colors.g, colors.b, 255]);
      Render.GradientRect(mp[0] + mp[2] + 6, mp[1] - 2, 1, mp[3] + 4, 0, [colors.b, colors.g, colors.r, 255], [colors.r, colors.g, colors.b, 255]);
      Render.GradientRect(mp[0] + mp[2] + 7, mp[1], 1, mp[3], 0, [colors.b, colors.g, colors.r, 255], [colors.r, colors.g, colors.b, 255]);
  
      Render.GradientRect(mp[0] - 4, mp[1] - 6, mp[2] + 8, 1, 1, [colors.r, colors.g, colors.b, 255], [colors.b, colors.g, colors.r, 255]);
      Render.GradientRect(mp[0] - 2, mp[1] - 7, mp[2] + 4, 1, 1, [colors.r, colors.g, colors.b, 255], [colors.b, colors.g, colors.r, 255]);
      Render.GradientRect(mp[0], mp[1] - 8, mp[2], 1, 1, [colors.r, colors.g, colors.b, 255], [colors.b, colors.g, colors.r, 255]);
  
      Render.GradientRect(mp[0] - 4, mp[1] + mp[3] + 5, mp[2] + 8, 1, 1, [colors.b, colors.g, colors.r, 255], [colors.r, colors.g, colors.b, 255]);
      Render.GradientRect(mp[0] - 2, mp[1] + mp[3] + 6, mp[2] + 4, 1, 1, [colors.b, colors.g, colors.r, 255], [colors.r, colors.g, colors.b, 255]);
      Render.GradientRect(mp[0], mp[1] + mp[3] + 7, mp[2], 1, 1, [colors.b, colors.g, colors.r, 255], [colors.r, colors.g, colors.b, 255]);
  }
  ```

- 448-485 paste自https://www.onetap.com/threads/release-screen-crosshair-hitmarker.31745/

  ```javascript
  var shot_data = [];
  
  function player_hurt() {
  
      attacker = Event.GetInt("attacker");
      attacker_entindex = Entity.GetEntityFromUserID(attacker);
  
      victim = Event.GetInt("userid");
      victim_entindex = Entity.GetEntityFromUserID(victim);
  
      if (attacker_entindex != Entity.GetLocalPlayer()) return;
  
      shot_data = [true, 255, Event.GetString("health")];
  
  }
  
  function on_paint() {
      if (UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Crosshair hitmarker"])) {
          var screen_size = Global.GetScreenSize();
          if (shot_data[0]) {
              shot_data[1] = shot_data[1] - 5;
  
              if (shot_data[1] <= 0) {
                  shot_data[0] = false;
              }
              var a = 4;
              var b = a + 6;
              var red = [255, 0, 0, shot_data[1]]
              var white = [255, 255, 255, shot_data[1]]
              var color = shot_data[2] <= 0 ? red : white;
  
              Render.Line(screen_size[0] / 2 - b, screen_size[1] / 2 - b, screen_size[0] / 2 - a, screen_size[1] / 2 - a, color); //Left Upper
              Render.Line(screen_size[0] / 2 - b, screen_size[1] / 2 + b, screen_size[0] / 2 - a, screen_size[1] / 2 + a, color); //Left Down
              Render.Line(screen_size[0] / 2 + b, screen_size[1] / 2 + b, screen_size[0] / 2 + a, screen_size[1] / 2 + a, color); //Right Down
              Render.Line(screen_size[0] / 2 + b, screen_size[1] / 2 - b, screen_size[0] / 2 + a, screen_size[1] / 2 - a, color); //Right Upper      
          }
      }
  }
  ```

- 556-598 投票显示 https://www.onetap.com/threads/vote-reveal-v4.31741/

  ```javascript
  var options = []
  
  function onVoteOptions() {
      options[0] = Event.GetString("option1")
      options[1] = Event.GetString("option2")
      options[2] = Event.GetString("option3")
      options[3] = Event.GetString("option4")
      options[4] = Event.GetString("option5")
  }
  
  function onVoteCast() {
      if (UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Vote Logs"])) {
          var entid = Event.GetInt("entityid");
          if (entid) {
              var team = Event.GetInt("team");
              var option = Event.GetInt("vote_option");
              var name = Entity.GetName(entid);
              var chTeam = "null";
              switch (team) {
                  case 0:
                      chTeam = "[N] ";
                      break;
                  case 1:
                      chTeam = "[S] ";
                      break;
                  case 2:
                      chTeam = "[T] ";
                      break;
                  case 3:
                      chTeam = "[CT] ";
                      break;
                  default:
                      chTeam = "[UNK] ";
                      break;
              }
  
              var vote = options[option];
              Global.PrintColor([217, 217, 217, 255], "[PASTED config] \0");
              Global.Print(chTeam + name + " voted " + vote + "\n");
              Global.PrintChat("\x01[ Control\x06sense\x01 ] \x04" + chTeam + name + " \x01投票 " + vote);
          }
      }
  }
  ```


- 605-684 Buylog https://www.onetap.com/threads/buy-logs-in-chat.31516/ 汉化部分用了最蠢的办法（没办法，只能paste怎么办）

  ```javascript
  function BuyLogs() {
      if (UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Buy Logs"]) && UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Log in chat"])) {
          var ent = Entity.GetEntityFromUserID(Event.GetInt('userid'))
          var team = Event.GetInt('team')
          if (team != Entity.GetProp(Entity.GetLocalPlayer(), "CBaseEntity", "m_iTeamNum")) {
              var item = Event.GetString('weapon')
              //去掉后缀
              item = item.replace("weapon_", "")
              item = item.replace("item_", "")
               
              //装备
              item = item.replace("assaultsuit", "防弹衣 + 防弹头盔")   
              item = item.replace("kevlar", "防弹衣")
              item = item.replace("taser", "电击枪")
              item = item.replace("defuser", "拆弹工具包")
              item = item.replace("cutters", "营救工具包")
  
              //手雷
              item = item.replace("hegrenade", "高爆手雷")
              item = item.replace("incgrenade", "燃烧弹")
              item = item.replace("molotov", "燃烧弹")
              item = item.replace("smokegrenade", "烟雾弹")
              item = item.replace("flashbang", "闪光弹")
              item = item.replace("decoy", "诱饵手雷")   
  
              //狙
              item = item.replace("ssg08", "鸟狙")
              item = item.replace("awp", "大狙")
              item = item.replace("g3sg1", "匪家连狙")
              item = item.replace("scar20", "警家连狙")
              
              //步枪
              item = item.replace("galilar", "加利尔 AR")
              item = item.replace("famas", "法玛斯")
              item = item.replace("ak47", "AK-47")
              item = item.replace("m4a1", "M4A4")
              item = item.replace("m4a1_silencer", "M4A1 消音型")
              item = item.replace("sg556", "SG 553")   
              item = item.replace("aug", "AUG")   
  
              //冲锋枪
              item = item.replace("mp9", "MP9")
              item = item.replace("mac10", "匪家吹风机")
              item = item.replace("mp7", "警家吹风机")
              item = item.replace("mp5sd", "MP5-SD")
              item = item.replace("ump45", "UMP-45")
              item = item.replace("p90", "P90")   
              item = item.replace("bizon", "PP-野牛")   
  
              //重武器
              item = item.replace("nova", "新星")
              item = item.replace("xm1014", "XM1014")
              item = item.replace("mag7", "MGA-7")
              item = item.replace("sawedoff", "截短霰弹枪")
              item = item.replace("m249", "M249")
              item = item.replace("negev", "内格夫")   
  
              //手枪
              item = item.replace("glock", "格洛克 18 型")
              item = item.replace("p2000", "P2000")
              item = item.replace("usp_silencer", "USP 消音版")
              item = item.replace("elite", "双枪")
              item = item.replace("p250", "P250")
              item = item.replace("fiveseven", "FN57")   
              item = item.replace("tec9", "TEC-9")   
              item = item.replace("cz75a", "CZ75 自动手枪")
              item = item.replace("deagle", "沙漠之鹰")   
              item = item.replace("revolver", "R8 左轮手枪")   
  
              if (item != "unknown") {
                  var name = Entity.GetName(ent)
                  var tickcount = Global.Tickcount();
                  var color = RGB(tickcount % 350 / 350, 1, 1, 1, 255);
  
                  Global.PrintChat(" \x01[ Control\x06sense\x01 ] \x04" + name + " \x01购买了 \x04" + item + " \n");
                  Cheat.PrintColor([color.r, color.g, color.b, 255], " \x01[ Control\x06sense\x01 ] \x06" + name + " \x01购买了 \x04" + item + " \n");
              }
          }
      }
  }
  ```

- hit log (这玩意版本太多了 只能说paste完改了很大部分)

- 919-1034 C4指示器

  ```javascript
  function calcDist(local, target) {
      var lx = local[0];
      var ly = local[1];
      var lz = local[2];
      var tx = target[0];
      var ty = target[1];
      var tz = target[2];
      var dx = lx - tx;
      var dy = ly - ty;
      var dz = lz - tz;
  
      return Math.sqrt(dx * dx + dy * dy + dz * dz);
  }
  
  function dispDamage() {
      local = Entity.GetLocalPlayer();
  
      if (!UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Enable C4 Indicator"])) return;
      var c4 = Entity.GetEntitiesByClassID(128)[0];
  
      if (c4 == undefined) return;
  
      var eLoc = Entity.GetRenderOrigin(c4);
      var lLoc = Entity.GetRenderOrigin(local)
      var distance = calcDist(eLoc, lLoc);
      var willKill = false;
      var dmg;
      //player checks
      var armor = Entity.GetProp(local, "CCSPlayerResource", "m_iArmor"); // player armor
      var health = Entity.GetProp(local, "CBasePlayer", "m_iHealth"); // player health
      //c4 things
      var timer = (Entity.GetProp(c4, "CPlantedC4", "m_flC4Blow") - Globals.Curtime()); // c4 left time
      var c4length = Entity.GetProp(c4, "CPlantedC4", "m_flTimerLength");
      var isbombticking = Entity.GetProp(c4, "CPlantedC4", "m_bBombTicking");
      //defusing things
      var deflength = Entity.GetProp(c4, "CPlantedC4", "m_flDefuseLength"); // length of defuse
      var deftimer = (Entity.GetProp(c4, "CPlantedC4", "m_flDefuseCountDown") - Globals.Curtime()); // timer when defusing
      var defbarlength = (((Render.GetScreenSize()[1] - 50) / deflength) * (deftimer)); // lenght for left bar
      var isbeingdefused = Entity.GetProp(c4, "CPlantedC4", "m_hBombDefuser"); // check if bomb is being defused
      var gotdefused = Entity.GetProp(c4, "CPlantedC4", "m_bBombDefused"); // check if bomb has or hasnt defused
  
      const a = 450.7;
      const b = 75.68;
      const c = 789.2;
  
      const d = (distance - b) / c;
  
      var damage = a * Math.exp(-d * d);
  
      if (armor > 0) {
          var newDmg = damage * 0.5;
          var armorDmg = (damage - newDmg) * 0.5;
  
          if (armorDmg > armor) {
              armor = armor * (1 / .5);
              newDmg = damage - armorDmg;
          }
          damage = newDmg;
      }
      dmg = Math.ceil(damage);
  
      if (dmg >= health) {
          willKill = true;
      } else {
          willKill = false;
      }
  
      timer = parseFloat(timer.toPrecision(3));
      timer2 = parseFloat(timer.toPrecision(2));
      timer3 = parseFloat(timer.toPrecision(1));
      bomb_font = Render.AddFont("Verdana", 16, 800);
  
      if (!isbombticking) return;
  
      if (gotdefused) return;
      if (timer >= 1 && timer > 10) {
          Render.String(10 + 1, 5 + 1, 0, getSite(c4) + timer + "s", [0, 0, 0, 255], bomb_font);
          Render.String(10, 5, 0, getSite(c4) + timer + "s", [129, 177, 14, 255], bomb_font);
      } else if (timer <= 10 && timer > 5 && timer >= 1) {
          Render.String(10 + 1, 5 + 1, 0, getSite(c4) + timer2 + "s", [0, 0, 0, 255], bomb_font);
          Render.String(10, 5, 0, getSite(c4) + timer2 + "s", [210, 216, 112, 255], bomb_font);
      } else if (timer <= 5 && timer >= 1) {
          Render.String(10 + 1, 5 + 1, 0, getSite(c4) + timer2 + "s", [0, 0, 0, 255], bomb_font);
          Render.String(10, 5, 0, getSite(c4) + timer2 + "s", [252, 18, 19, 255], bomb_font);
      } else if (timer < 1 && timer >= 0.1) {
          Render.String(10 + 1, 5 + 1, 0, getSite(c4) + timer3 + "s", [0, 0, 0, 255], bomb_font);
          Render.String(10, 5, 0, getSite(c4) + timer3 + "s", [252, 18, 19, 255], bomb_font);
      }
      // defuse time bar
      if (isbeingdefused > 0) {
          if (timer > deflength && timer >= 0.1) {
              Render.FilledRect(0, 0, 15, defbarlength, [58, 191, 54, 120]);
          } else {
              Render.FilledRect(0, 0, 15, defbarlength, [252, 18, 19, 120]);
          }
      }
  
      if (!Entity.IsAlive(local)) return;
      if (willKill) {
          Render.String(10 + 1, 25 + 1, 0, "Kill", [0, 0, 0, 200], bomb_font);
          Render.String(10, 25, 0, "Kill", [252, 18, 19, 200], bomb_font);
      } else if (damage > 0.5) {
          Render.String(10 + 1, 25 + 1, 0, "-" + dmg + "HP", [0, 0, 0, 255], bomb_font);
          Render.String(10, 25, 0, "-" + dmg + "HP", [210, 216, 112, 255], bomb_font);
      }
  }
  
  function getSite(c4) {
      bombsite = Entity.GetProp(c4, "CPlantedC4", "m_nBombSite");
  
      if (bombsite == 0) {
          return "A - ";
      } else {
          return "B - ";
      }
  }
  
  ```

- 获取武器对应onetap的名称

  ```javascript
  var nameList = {
      1: "Deagle",
      2: "Dualies",
      3: "Five Seven",
      4: "Glock",
      7: "AK47",
      8: "AUG",
      9: "AWP",
      10: "FAMAS",
      11: "G3SG1",
      13: "GALIL",
      14: "M249",
      16: "M4A4",
      17: "Mac10",
      19: "P90",
      23: "MP5",
      24: "UMP45",
      25: "XM1014",
      26: "PP-Bizon",
      27: "MAG7",
      28: "Negev",
      29: "Sawed off",
      30: "Tec-9",
      32: "P2000",
      33: "MP7",
      34: "MP9",
      35: "Nova",
      36: "P250",
      38: "SCAR20",
      39: "SG553",
      40: "SSG08",
      60: "M4A1-S",
      61: "USP",
      63: "CZ-75",
      64: "Revolver",
  
  };
  
  function getCurrentWeapon(player) {
      if (!Entity.IsAlive(player)) return "General";
      weapon = Entity.GetProp(player, "CBasePlayer", "m_hActiveWeapon");
      if (weapon == "m_hActiveWeapon") return "General";
      weapon = (Entity.GetProp(weapon, "CBaseAttributableItem", "m_iItemDefinitionIndex") & 0xFFFF);
  
      if (nameList[weapon] != undefined) {
          return nameList[weapon];
      } else if (nameList[weapon] == undefined) {
          return "General";
      }
  }
  
  ```

- 1175-1208 DT充能 https://www.onetap.com/threads/release-increase-dt-recharge-speed.32428/

  ```javascript
  function can_shift_shot(ticks_to_shift) {
      var me = Entity.GetLocalPlayer();
      var wpn = Entity.GetWeapon(me);
  
      if (me == null || wpn == null)
          return false;
  
      var tickbase = Entity.GetProp(me, "CCSPlayer", "m_nTickBase");
      var curtime = Globals.TickInterval() * (tickbase - ticks_to_shift)
  
      if (curtime < Entity.GetProp(me, "CCSPlayer", "m_flNextAttack"))
          return false;
  
      if (curtime < Entity.GetProp(wpn, "CBaseCombatWeapon", "m_flNextPrimaryAttack"))
          return false;
  
      return true;
  }
  
  function _TBC_CREATE_MOVE() {
      if (UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Better DT recharge"])) {
          var is_charged = Exploit.GetCharge()
  
          Exploit[(is_charged != 1 ? "Enable" : "Disable") + "Recharge"]()
  
          if (can_shift_shot(14) && is_charged != 1) {
              Exploit.DisableRecharge();
              Exploit.Recharge()
          }
  
          Exploit.OverrideTolerance(1);
          Exploit.OverrideShift(17);
      }
  }
  
  ```

- 1215-1229 空中命中率 https://www.onetap.com/threads/air-hitchance-scout-r8-deset-eagle-awp-scar.34487/ （不得不说这b很搞笑，paste的部分自己和自己冲突，明明下面的武器里有空中命中率覆盖还又paste进一个空中命中率属实搞笑）

  ```javascript
  function AirHitchance() {
      if (!UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Jump Scout/Revolver Hitchance"])) {
          return
      };
      var weapons = Entity.GetName(Entity.GetWeapon(Entity.GetLocalPlayer()));
      if (weapons != 'ssg 08' && weapons != 'r8 revolver') {
          return
      };
      var flags = Entity.GetProp(Entity.GetLocalPlayer(), 'CBasePlayer', 'm_fFlags');
      if (!(flags & 1 << 0) && !(flags & 1 << 18)) {
          target = Ragebot.GetTarget();
          value = UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", 'Hitchance']);
          Ragebot.ForceTargetHitchance(target, value);
      }
  }
  ```

- 第三人称摄像机视角 paste自老版本dhdj.js （老到还是一坨狗屎的版本）

  ```javascript
  function Draw_freecamera() {
      localPlayer = Entity.GetLocalPlayer();
      if (UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Enable free camera"])) {
          delayCamera();
      }
  }
  
  //-------------------------------------------------------------------------------
  var camerPASTEData = [
      [
          [0, 0, 0],
          [0, 0, 0]
      ],
      [
          [0, 0, 0],
          [0, 0, 0]
      ],
      [
          [0, 0, 0],
          [0, 0, 0]
      ],
      [
          [0, 0, 0],
          [0, 0, 0]
      ],
      [
          [0, 0, 0],
          [0, 0, 0]
      ],
      [
          [0, 0, 0],
          [0, 0, 0]
      ],
      [
          [0, 0, 0],
          [0, 0, 0]
      ],
      [
          [0, 0, 0],
          [0, 0, 0]
      ],
      [
          [0, 0, 0],
          [0, 0, 0]
      ],
      [
          [0, 0, 0],
          [0, 0, 0]
      ],
      [
          [0, 0, 0],
          [0, 0, 0]
      ],
      [
          [0, 0, 0],
          [0, 0, 0]
      ],
      [
          [0, 0, 0],
          [0, 0, 0]
      ],
      [
          [0, 0, 0],
          [0, 0, 0]
      ],
      [
          [0, 0, 0],
          [0, 0, 0]
      ],
      [
          [0, 0, 0],
          [0, 0, 0]
      ],
      [
          [0, 0, 0],
          [0, 0, 0]
      ],
      [
          [0, 0, 0],
          [0, 0, 0]
      ],
      [
          [0, 0, 0],
          [0, 0, 0]
      ],
      [
          [0, 0, 0],
          [0, 0, 0]
      ],
      [
          [0, 0, 0],
          [0, 0, 0]
      ],
      [
          [0, 0, 0],
          [0, 0, 0]
      ],
      [
          [0, 0, 0],
          [0, 0, 0]
      ],
      [
          [0, 0, 0],
          [0, 0, 0]
      ],
      [
          [0, 0, 0],
          [0, 0, 0]
      ],
      [
          [0, 0, 0],
          [0, 0, 0]
      ],
      [
          [0, 0, 0],
          [0, 0, 0]
      ],
      [
          [0, 0, 0],
          [0, 0, 0]
      ],
      [
          [0, 0, 0],
          [0, 0, 0]
      ],
      [
          [0, 0, 0],
          [0, 0, 0]
      ],
      [
          [0, 0, 0],
          [0, 0, 0]
      ],
      [
          [0, 0, 0],
          [0, 0, 0]
      ]
  ];
  var lastFrameCamera = [0, 0, 0];
  var thirdDistance = UI.GetValue(["Misc.", "View", "General", "Thirdperson Distance"]) - 20;
  
  function delayCamera() {
      if (UI.GetValue(["Rage", "Anti Aim", "General", "Key assignment", "Fake duck"]) && UI.GetValue(["Config", "SUBTAB_MGR", "Scripts", "SHEET_MGR", "Keys", "JS Keybinds", "[FD]Keybind"]) && !Entity.IsAlive(localPlayer)) {
          camerPASTEData = [
              [
                  [0, 0, 0],
                  [0, 0, 0]
              ],
              [
                  [0, 0, 0],
                  [0, 0, 0]
              ],
              [
                  [0, 0, 0],
                  [0, 0, 0]
              ],
              [
                  [0, 0, 0],
                  [0, 0, 0]
              ],
              [
                  [0, 0, 0],
                  [0, 0, 0]
              ],
              [
                  [0, 0, 0],
                  [0, 0, 0]
              ],
              [
                  [0, 0, 0],
                  [0, 0, 0]
              ],
              [
                  [0, 0, 0],
                  [0, 0, 0]
              ],
              [
                  [0, 0, 0],
                  [0, 0, 0]
              ],
              [
                  [0, 0, 0],
                  [0, 0, 0]
              ],
              [
                  [0, 0, 0],
                  [0, 0, 0]
              ],
              [
                  [0, 0, 0],
                  [0, 0, 0]
              ],
              [
                  [0, 0, 0],
                  [0, 0, 0]
              ],
              [
                  [0, 0, 0],
                  [0, 0, 0]
              ],
              [
                  [0, 0, 0],
                  [0, 0, 0]
              ],
              [
                  [0, 0, 0],
                  [0, 0, 0]
              ],
              [
                  [0, 0, 0],
                  [0, 0, 0]
              ],
              [
                  [0, 0, 0],
                  [0, 0, 0]
              ],
              [
                  [0, 0, 0],
                  [0, 0, 0]
              ],
              [
                  [0, 0, 0],
                  [0, 0, 0]
              ],
              [
                  [0, 0, 0],
                  [0, 0, 0]
              ],
              [
                  [0, 0, 0],
                  [0, 0, 0]
              ],
              [
                  [0, 0, 0],
                  [0, 0, 0]
              ],
              [
                  [0, 0, 0],
                  [0, 0, 0]
              ],
              [
                  [0, 0, 0],
                  [0, 0, 0]
              ],
              [
                  [0, 0, 0],
                  [0, 0, 0]
              ],
              [
                  [0, 0, 0],
                  [0, 0, 0]
              ],
              [
                  [0, 0, 0],
                  [0, 0, 0]
              ],
              [
                  [0, 0, 0],
                  [0, 0, 0]
              ],
              [
                  [0, 0, 0],
                  [0, 0, 0]
              ],
              [
                  [0, 0, 0],
                  [0, 0, 0]
              ],
              [
                  [0, 0, 0],
                  [0, 0, 0]
              ]
          ];
          lastFrameCamera = [0, 0, 0];
          return;
      }
      eyePos = Entity.GetEyePosition(localPlayer);
      angles = Local.GetViewAngles();
      angles[0] = angles[0] * -1;
      if (angles[1] > 0) {
          angles[1] = angles[1] - 180;
      } else {
          angles[1] = 180 + angles[1];
      }
      camerPASTEData.pop();
      camerPASTEData.unshift([eyePos, angles]);
  }
  
  function showDelayedCamera() {
      if (UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Enable free camera"]) && camerPASTEData[UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Max free camera follow value"]) - 1][0][0] != 0 && UI.GetValue(["Misc.", "Keys", "General", "Key assignment", "Thirdperson"]) == 1 && UI.GetValue(["Rage", "Anti Aim", "General", "Key assignment", "Fake duck"]) == 0 && UI.GetValue(["Config", "SUBTAB_MGR", "Scripts", "SHEET_MGR", "Keys", "JS Keybinds", "[FD]Keybind"]) == 0 && Entity.IsAlive(localPlayer)) {
          eyePos = camerPASTEData[UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Max free camera follow value"]) - 1][0];
          angles = camerPASTEData[UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Max free camera follow value"]) - 1][1];
          vector = ANGLE2VEC(angles);
          cameraPos = [eyePos[0] + vector[0] * thirdDistance, eyePos[1] + vector[1] * thirdDistance, eyePos[2] + vector[2] * thirdDistance];
          Local.SetCameraPosition(cameraPos);
          lastFrameCamera = cameraPos;
      }
  }
  
  function calcDelayedCamera() {
      if (UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Enable free camera"]) && camerPASTEData[UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Max free camera follow value"]) - 1][0][0] != 0 && UI.GetValue(["Misc.", "Keys", "General", "Key assignment", "Thirdperson"]) == 1 && UI.GetValue(["Rage", "Anti Aim", "General", "Key assignment", "Fake duck"]) == 0 && UI.GetValue(["Config", "SUBTAB_MGR", "Scripts", "SHEET_MGR", "Keys", "JS Keybinds", "[FD]Keybind"]) == 0 && Entity.IsAlive(localPlayer)) {
          angles = camerPASTEData[UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Max free camera follow value"]) - 1][1];
          back = getWallDistance(localPlayer, angles);
          thirdDistance = UI.GetValue(["Misc.", "View", "General", "Thirdperson Distance"]) - 10
          if (getVelocity(Entity.GetLocalPlayer()) > 90) {
              var a = 16
          }
          if (getVelocity(Entity.GetLocalPlayer()) < 91) {
              var a = 12
          }
          if (back < thirdDistance) {
              thirdDistance = back - a;
          }
          showDelayedCamera();
      }
  }
  ```

  

- 1653-1688 health shot effect

  ```javascript
  var alpha = 0;
  var size = 0;
  
  function clamp(v, min, max) {
      return Math.max(Math.min(v, max), min);
  }
  
  function get(element) {
      return UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Hit effect"], element);
  }
  
  function render_effect() {
      if (alpha === 0)
          return;
  
      const inc_alpha = ((1 / get("kill effect")) * Global.Frametime()) * 255
      const inc_size = ((1 / get("kill effect")) * Global.Frametime()) * 360
  
      alpha = clamp(alpha - inc_alpha, 0, 255);
      size = clamp(size - inc_size, 0, 360);
  
      const x = Global.GetScreenSize()[0],
          y = Global.GetScreenSize()[1];
  
      Render.GradientRect(0, 0, x, size, 0, [128, 195, 255, alpha], [128, 195, 255, 0]);
      Render.GradientRect(0, y - size, x, size, 0, [128, 195, 255, 0], [128, 195, 255, alpha]);
      Render.GradientRect(x - size, 0, size, y, 1, [128, 195, 255, 0], [128, 195, 255, alpha]);
      Render.GradientRect(0, 0, size, y, 1, [128, 195, 255, alpha], [128, 195, 255, 0]);
  }
  
  function on_death() {
      if (Entity.IsLocalPlayer(Entity.GetEntityFromUserID(Event.GetInt("attacker")))) {
          alpha = 220;
          size = 180;
      }
  }
  ```

  

- 1744-1815 子弹射线 paste自老版本dhdj.js

  ```javascript
  var bullets = [];
  var screen_size_local = Global.GetScreenSize();
  
  function draw_local() {
      if (UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Show Bullet Tracer"])) drawBulletTracer();
      var tickcount = Global.Tickcount();
      var color = RGB(tickcount % 350 / 350, 1, 1, 1, 255);
      if (UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "RGB Tracer Color"])) {
          UI.SetColor(["Config", "PASTED menu misc.", "PASTED menu misc.", "Bullet Tracer Color"], [color.r, color.g, color.b, 160])
      }
  }
  
  function UI_onBulletImpact() {
      if (!UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Show Bullet Tracer"])) return;
      player = Entity.GetEntityFromUserID(Event.GetInt("userid"));
      if (Entity.GetLocalPlayer() !== player) return;
      if (bullets.length > 20) bullets = [];
      eyePos = Entity.GetEyePosition(Entity.GetLocalPlayer());
      vector = [Event.GetFloat("x") - eyePos[0], Event.GetFloat("y") - eyePos[1], Event.GetFloat("z") - eyePos[2]];
      eyePos[0] += vector[0] * 0.01;
      eyePos[1] += vector[1] * 0.01;
      eyePos[2] += vector[2] * 0.01;
      bullets.push({
          "impact": [Event.GetFloat("x"), Event.GetFloat("y"), Event.GetFloat("z")],
          "origin": eyePos,
          "time": Globals.Curtime()
      });
  }
  
  function duplicate(theObject) {
      return JSON.parse(JSON.stringify(theObject));
  }
  
  function getDistance(A, B) {
      return Math.sqrt(Math.pow(A[0] - B[0], 2) + Math.pow(A[1] - B[1], 2) + Math.pow(A[2] - B[2], 2));
  }
  
  function drawBulletTracer() {
      var me = Entity.GetLocalPlayer();
      if (bullets.length < 1) return;
      for (i = 0; i < bullets.length; i++) {
          if (bullets[i] != undefined) {
              if (bullets[i]["time"] + 2 < Globals.Curtime()) {
                  delete bullets[i];
              } else {
                  impact = Render.WorldToScreen(bullets[i]["impact"]);
                  origin = Render.WorldToScreen(bullets[i]["origin"]);
                  if (origin != undefined && impact != undefined) {
                      if (origin[2] == 0 && !UI.GetValue(["Misc.", "Keys", "General", "Key assignment", "Thirdperson"]) && Entity.IsAlive(me)) {
                          vector = [bullets[i]["impact"][0] - bullets[i]["origin"][0], bullets[i]["impact"][1] - bullets[i]["origin"][1], bullets[i]["impact"][2] - bullets[i]["origin"][2]];
                          newOrigin = duplicate(bullets[i]["origin"]);
                          length = getDistance(bullets[i]["impact"], newOrigin) - getDistance(bullets[i]["impact"], Entity.GetEyePosition(Entity.GetLocalPlayer()));
                          newOrigin[0] += vector[0] * (length / getDistance(bullets[i]["impact"], newOrigin) + 0.05);
                          newOrigin[1] += vector[1] * (length / getDistance(bullets[i]["impact"], newOrigin) + 0.05);
                          newOrigin[2] += vector[2] * (length / getDistance(bullets[i]["impact"], newOrigin) + 0.05);
                          origin = Render.WorldToScreen(newOrigin);
                      }
                      if (origin[1] < screen_size_local[1] && origin[0] < screen_size_local[0] && origin[0] > 0 && Entity.IsAlive(me)) {
                          Render.Line(impact[0], impact[1], origin[0], origin[1], UI.GetColor(["Config", "PASTED menu misc.", "PASTED menu misc.", "Bullet Tracer Color"]));
                          step = Math.floor(UI.GetColor(["Config", "PASTED menu misc.", "PASTED menu misc.", "Bullet Tracer Color"])[3] / UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Bullet Tracer Thickness"]));
                          for (x = 1; x < UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Bullet Tracer Thickness"]); x++) {
                              Render.Line(impact[0] + (x - 1), impact[1], origin[0] + x, origin[1], [UI.GetColor(["Config", "PASTED menu misc.", "PASTED menu misc.", "Bullet Tracer Color"])[0], UI.GetColor(["Config", "PASTED menu misc.", "PASTED menu misc.", "Bullet Tracer Color"])[1], UI.GetColor(["Config", "PASTED menu misc.", "PASTED menu misc.", "Bullet Tracer Color"])[2], UI.GetColor(["Config", "PASTED menu misc.", "PASTED menu misc.", "Bullet Tracer Color"])[3] - (x * step)]);
                              Render.Line(impact[0], impact[1] + (x - 1), origin[0], origin[1] + x, [UI.GetColor(["Config", "PASTED menu misc.", "PASTED menu misc.", "Bullet Tracer Color"])[0], UI.GetColor(["Config", "PASTED menu misc.", "PASTED menu misc.", "Bullet Tracer Color"])[1], UI.GetColor(["Config", "PASTED menu misc.", "PASTED menu misc.", "Bullet Tracer Color"])[2], UI.GetColor(["Config", "PASTED menu misc.", "PASTED menu misc.", "Bullet Tracer Color"])[3] - (x * step)]);
                              Render.Line(impact[0] - (x - 1), impact[1], origin[0] - x, origin[1], [UI.GetColor(["Config", "PASTED menu misc.", "PASTED menu misc.", "Bullet Tracer Color"])[0], UI.GetColor(["Config", "PASTED menu misc.", "PASTED menu misc.", "Bullet Tracer Color"])[1], UI.GetColor(["Config", "PASTED menu misc.", "PASTED menu misc.", "Bullet Tracer Color"])[2], UI.GetColor(["Config", "PASTED menu misc.", "PASTED menu misc.", "Bullet Tracer Color"])[3] - (x * step)]);
                              Render.Line(impact[0], impact[1] - (x - 1), origin[0], origin[1] - x, [UI.GetColor(["Config", "PASTED menu misc.", "PASTED menu misc.", "Bullet Tracer Color"])[0], UI.GetColor(["Config", "PASTED menu misc.", "PASTED menu misc.", "Bullet Tracer Color"])[1], UI.GetColor(["Config", "PASTED menu misc.", "PASTED menu misc.", "Bullet Tracer Color"])[2], UI.GetColor(["Config", "PASTED menu misc.", "PASTED menu misc.", "Bullet Tracer Color"])[3] - (x * step)]);
                          }
                      }
                  }
              }
          }
      }
  }
  ```

  

- 假蹲 (蹲的部分就不说了，都满天飞的v3时代js) 2134-2163 假蹲视角固定 我寻思这玩意也不难啊，IQ得多低才能只靠paste啊

  ```javascript
  
  var maxLevel = 25;
  var valve_1 = false;
  function fastDuckUpdate() {
      valve_1 = Entity.GetProp(Entity.GetGameRulesProxy(), "CCSGameRulesProxy", "m_bIsValveDS");
      if (valve_1) {
          if (UI.GetValue(["Config", "SUBTAB_MGR", "Scripts", "SHEET_MGR", "Keys", "JS Keybinds", "[FD]Keybind"])) {
              var eyePos_1 = Entity.GetEyePosition(localPlayer);
              var origin_1 = Entity.GetRenderOrigin(localPlayer);
              eyePos_1[2] = origin_1[2] + 46 + (18 - (maxLevel + 1) / 100 * 18);
              if (UI.GetValue(["Misc.", "Keys", "General", "Key assignment", "Thirdperson"]) == 1) {
                  var angles_1 = Local.GetViewAngles();
                  angles_1[0] = angles_1[0] * -1;
                  if (angles_1[1] > 0) {
                      angles_1[1] = angles_1[1] - 180;
                  } else {
                      angles_1[1] = 180 + angles_1[1];
                  }
                  var back_1 = getWallDistance(localPlayer, angles_1);
                  var angles_1 = ANGLE2VEC(angles_1);
                  var thirdDistance_1 = UI.GetValue(["Misc.", "View", "General", "Thirdperson Distance"]);
                  if (back_1 < thirdDistance_1) {
                      thirdDistance_1 = back_1 - 10;
                  }
                  Local.SetCameraPosition([eyePos_1[0] + angles_1[0] * thirdDistance_1, eyePos_1[1] + angles_1[1] * thirdDistance_1, eyePos_1[2] + angles_1[2] * thirdDistance_1]);
              } else {
                  Local.SetCameraPosition([eyePos_1[0], eyePos_1[1], eyePos_1[2]]);
              }
          }
      }
  }
  ```

  

- 2852-3021 anti bruteforce （我记得这玩意是Vex写的）

  ```javascript
  function GetScriptOption(name) {
      var Value = UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "Anti Bruteforce"], name);
      return Value;
  }
  
  function radian(degree) {
      return degree * Math.PI / 180.0;
  }
  
  function ExtendVector(vector, angle, extension) {
      var radianAngle = radian(angle);
      return [extension * Math.cos(radianAngle) + vector[0], extension * Math.sin(radianAngle) + vector[1], vector[2]];
  }
  
  function VectorAdd(a, b) {
      return [a[0] + b[0], a[1] + b[1], a[2] + b[2]];
  }
  
  function VectorSubtract(a, b) {
      return [a[0] - b[0], a[1] - b[1], a[2] - b[2]];
  }
  
  function VectorMultiply(a, b) {
      return [a[0] * b[0], a[1] * b[1], a[2] * b[2]];
  }
  
  function VectorLength(x, y, z) {
      return Math.sqrt(x * x + y * y + z * z);
  }
  
  function VectorNormalize(vec) {
      var length = VectorLength(vec[0], vec[1], vec[2]);
      return [vec[0] / length, vec[1] / length, vec[2] / length];
  }
  
  function VectorDot(a, b) {
      return a[0] * b[0] + a[1] * b[1] + a[2] * b[2];
  }
  
  function VectorDistance(a, b) {
      return VectorLength(a[0] - b[0], a[1] - b[1], a[2] - b[2]);
  }
  
  function ClosestPointOnRay(target, rayStart, rayEnd) {
      var to = VectorSubtract(target, rayStart);
      var dir = VectorSubtract(rayEnd, rayStart);
      var length = VectorLength(dir[0], dir[1], dir[2]);
      dir = VectorNormalize(dir);
  
      var rangeAlong = VectorDot(dir, to);
      if (rangeAlong < 0.0) {
          return rayStart;
      }
      if (rangeAlong > length) {
          return rayEnd;
      }
      return VectorAdd(rayStart, VectorMultiply(dir, [rangeAlong, rangeAlong, rangeAlong]));
  }
  
  function Flip() {
      UI.ToggleHotkey(["Rage", "Anti Aim", "General", "Key assignment", "AA Direction inverter"], "AA Inverter");
  }
  
  var lastHitTime = 0.0;
  var lastImpactTimes = [
      0.0
  ];
  var lastImpacts = [
      [0.0, 0.0, 0.0]
  ];
  
  function OnHurt() {
      if (UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "Fakelag & Anti-Brute"])) {
          if (GetScriptOption("Anti Bruteforce") == 0) return;
          if (Entity.GetEntityFromUserID(Event.GetInt("userid")) !== Entity.GetLocalPlayer()) return;
          var hitbox = Event.GetInt('hitgroup');
  
          if (hitbox == 1 || hitbox == 6 || hitbox == 7) //head, both toe
          {
              var curtime = Global.Curtime();
              if (Math.abs(lastHitTime - curtime) > 0.5) //0.2s backtrack + 0.2 extand + 0.1 extra
              {
                  lastHitTime = curtime;
                  Flip();
              }
          }
      }
  }
  
  function OnBulletImpact() {
      if (UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "Fakelag & Anti-Brute"])) {
          if (GetScriptOption("Anti Bruteforce") !== 2) return;
  
          var curtime = Global.Curtime();
          if (Math.abs(lastHitTime - curtime) < 0.5) return;
  
          var entity = Entity.GetEntityFromUserID(Event.GetInt("userid"));
          var impact = [Event.GetFloat("x"), Event.GetFloat("y"), Event.GetFloat("z"), curtime];
          var source;
          if (Entity.IsValid(entity) && Entity.IsEnemy(entity)) {
              if (!Entity.IsDormant(entity)) {
                  source = Entity.GetEyePosition(entity);
              } else if (Math.abs(lastImpactTimes[entity] - curtime) < 0.1) {
                  source = lastImpacts[entity];
              } else {
                  lastImpacts[entity] = impact;
                  lastImpactTimes[entity] = curtime;
                  return;
              }
              var local = Entity.GetLocalPlayer();
              var localEye = Entity.GetEyePosition(local);
              var localOrigin = Entity.GetProp(local, "CBaseEntity", "m_vecOrigin");
              var localBody = VectorMultiply(VectorAdd(localEye, localOrigin), [0.5, 0.5, 0.5]);
  
              var bodyVec = ClosestPointOnRay(localBody, source, impact);
              var bodyDist = VectorDistance(localBody, bodyVec);
  
              if (bodyDist < 85.0) //he clearly shot at us!
              {
                  var realAngle = Local.GetRealYaw();
                  var fakeAngle = Local.GetFakeYaw();
  
                  var headVec = ClosestPointOnRay(localEye, source, impact);
                  var headDist = VectorDistance(localEye, headVec);
                  var feetVec = ClosestPointOnRay(localOrigin, source, impact);
                  var feetDist = VectorDistance(localOrigin, feetVec);
  
                  var closestRayPoint;
                  var realPos;
                  var fakePos;
  
                  if (bodyDist < headDist && bodyDist < feetDist) //that's a pelvis
                  { //pelvis direction = goalfeetyaw + 180    
                      closestRayPoint = bodyVec;
                      realPos = ExtendVector(bodyVec, realAngle + 180.0, 10.0);
                      fakePos = ExtendVector(bodyVec, fakeAngle + 180.0, 10.0);
                  } else if (feetDist < headDist) //ow my toe
                  { //toe direction = goalfeetyaw -30 +- 90
                      closestRayPoint = feetVec;
                      var realPos1 = ExtendVector(bodyVec, realAngle - 30.0 + 60.0, 10.0);
                      var realPos2 = ExtendVector(bodyVec, realAngle - 30.0 - 60.0, 10.0);
                      var fakePos1 = ExtendVector(bodyVec, fakeAngle - 30.0 + 60.0, 10.0);
                      var fakePos2 = ExtendVector(bodyVec, fakeAngle - 30.0 - 60.0, 10.0);
                      if (VectorDistance(feetVec, realPos1) < VectorDistance(feetVec, realPos2)) {
                          realPos = realPos1;
                      } else {
                          realPos = realPos2;
                      }
                      if (VectorDistance(feetVec, fakePos1) < VectorDistance(feetVec, fakePos2)) {
                          fakePos = fakePos1;
                      } else {
                          fakePos = fakePos2;
                      }
                  } else {
                      closestRayPoint = headVec;
                      realPos = ExtendVector(bodyVec, realAngle, 10.0);
                      fakePos = ExtendVector(bodyVec, fakeAngle, 10.0);
                  }
  
                  if (VectorDistance(closestRayPoint, fakePos) < VectorDistance(closestRayPoint, realPos)) {
                      lastHitTime = curtime;
                      Flip();
                  }
              }
  
              lastImpacts[entity] = impact;
              lastImpactTimes[entity] = curtime;
          }
      }
  }
  ```

- 3153-3187 freestanding paste自老版本dhdj.js

```javascript
UI.AddSubTab(["Config", "SUBTAB_MGR"], "[PASTED]Freestanding");
UI.AddSliderInt(["Config", "[PASTED]Freestanding", "[PASTED]Freestanding"], "--Warning: testing feature!!!--", 0, 0);
UI.AddCheckbox(["Config", "[PASTED]Freestanding", "[PASTED]Freestanding"], "Enable freestanding");
UI.AddDropdown(["Config", "[PASTED]Freestanding", "[PASTED]Freestanding"], "Freestanding Mode", ["Disabled", "Normal", "Reversed"], 0);

function setInvert(shouldInvert) {
    if (shouldInvert) {
        if (!UI.GetValue(["Rage", "Anti Aim", "General", "Key assignment", "AA Direction inverter"])) {
            UI.ToggleHotkey(["Rage", "Anti Aim", "General", "Key assignment", "AA Direction inverter"]);
        }
    } else {
        if (UI.GetValue(["Rage", "Anti Aim", "General", "Key assignment", "AA Direction inverter"])) {
            UI.ToggleHotkey(["Rage", "Anti Aim", "General", "Key assignment", "AA Direction inverter"]);
        }
    }
}

function Freestanding_() {
    angles = Local.GetViewAngles();
    right = getWallDistance(Entity.GetLocalPlayer(), [0, angles[1] + 60]);
    left = getWallDistance(Entity.GetLocalPlayer(), [0, angles[1] - 60]);
    front = getWallDistance(Entity.GetLocalPlayer(), [0, angles[1]]);
    diff = Math.abs(left - right);
    if (UI.GetValue(["Config", "[PASTED]Freestanding", "[PASTED]Freestanding", "Enable freestanding"])) {
        if (UI.GetValue(["Config", "[PASTED]Freestanding", "[PASTED]Freestanding", "Freestanding Mode"]) != 0) {
            if (front < 40) {
                if (UI.GetValue(["Config", "[PASTED]Freestanding", "[PASTED]Freestanding", "Freestanding Mode"]) == 2) {
                    setInvert(right < left);
                } else if (UI.GetValue(["Config", "[PASTED]Freestanding", "[PASTED]Freestanding", "Freestanding Mode"]) == 1) {
                    setInvert(left < right);
                }
            }
        }
    }
}
```

- 3259-3292 不能算是paste蛤但是搞了个大小，上面刚写完假走 下面又来一个假走 你搁这叠buff呢？

- 4026-5463 直接给老版本dhdj.js的武器完完整整复制来咯 爆笑了

  ```javascript
  var hitboxes = [
      'Generic',
      'Head',
      'Chest',
      'Stomach',
      'Left arm',
      'Right arm',
      'Left leg',
      'Right leg',
      'Body'
  ];
  nameList = {
      1: "Deagle",
      2: "Dualies",
      3: "Five Seven",
      4: "Glock",
      7: "AK47",
      8: "AUG",
      9: "AWP",
      10: "FAMAS",
      11: "G3SG1",
      13: "GALIL",
      14: "M249",
      16: "M4A4",
      17: "Mac10",
      19: "P90",
      23: "MP5",
      24: "UMP45",
      25: "XM1014",
      26: "PP-Bizon",
      27: "MAG7",
      28: "Negev",
      29: "Sawed off",
      30: "Tec-9",
      32: "P2000",
      33: "MP7",
      34: "MP9",
      35: "Nova",
      36: "P250",
      38: "SCAR20",
      39: "SG553",
      40: "SSG08",
      60: "M4A1-S",
      61: "USP",
      63: "CZ-75",
      64: "Revolver",
  
  };
  var weaponSettings = {
      "General": ["General", ["Visible", "Autowall", "Minimum", "Doubletap"],
          ["Visible", "Autowall", "Mindmg", "Doubletap"]
      ],
      "Negev": ["General", ["Visible", "Autowall", "Minimum", "Doubletap"],
          ["Visible", "Autowall", "Mindmg", "Doubletap"]
      ],
      "M249": ["General", ["Visible", "Autowall", "Minimum", "Doubletap"],
          ["Visible", "Autowall", "Mindmg", "Doubletap"]
      ],
      "MAG7": ["General", ["Visible", "Autowall", "Minimum"],
          ["Visible", "Autowall", "Mindmg"]
      ],
      "Sawed off": ["General", ["Visible", "Autowall", "Minimum"],
          ["Visible", "Autowall", "Mindmg"]
      ],
      "XM1014": ["General", ["Visible", "Autowall", "Minimum"],
          ["Visible", "Autowall", "Mindmg"]
      ],
      "Nova": ["General", ["Visible", "Autowall", "Minimum"],
          ["Visible", "Autowall", "Mindmg"]
      ],
      "G3SG1": ["Autosniper", ["Visible", "Autowall", "Minimum", "Doubletap"],
          ["Visible", "Autowall", "Mindmg", "Doubletap"]
      ],
      "SCAR20": ["Autosniper", ["Visible", "Autowall", "Minimum", "Doubletap"],
          ["Visible", "Autowall", "Mindmg", "Doubletap"]
      ],
      "AWP": ["AWP", ["Visible", "Autowall", "Minimum"],
          ["Visible", "Autowall", "Mindmg"]
      ],
      "AUG": ["General", ["Visible", "Autowall", "Minimum", "Doubletap"],
          ["Visible", "Autowall", "Mindmg", "Doubletap"]
      ],
      "SG553": ["General", ["Visible", "Autowall", "Minimum", "Doubletap"],
          ["Visible", "Autowall", "Mindmg", "Doubletap"]
      ],
      "SSG08": ["Scout", ["Visible", "Autowall", "Minimum"],
          ["Visible", "Autowall", "Mindmg"]
      ],
      "AK47": ["General", ["Visible", "Autowall", "Minimum", "Doubletap"],
          ["Visible", "Autowall", "Mindmg", "Doubletap"]
      ],
      "M4A4": ["General", ["Visible", "Autowall", "Minimum", "Doubletap"],
          ["Visible", "Autowall", "Mindmg", "Doubletap"]
      ],
      "M4A1-S": ["General", ["Visible", "Autowall", "Minimum", "Doubletap"],
          ["Visible", "Autowall", "Mindmg", "Doubletap"]
      ],
      "FAMAS": ["General", ["Visible", "Autowall", "Minimum", "Doubletap"],
          ["Visible", "Autowall", "Mindmg", "Doubletap"]
      ],
      "GALIL": ["General", ["Visible", "Autowall", "Minimum", "Doubletap"],
          ["Visible", "Autowall", "Mindmg", "Doubletap"]
      ],
      "PP-Bizon": ["General", ["Visible", "Autowall", "Minimum", "Doubletap"],
          ["Visible", "Autowall", "Mindmg", "Doubletap"]
      ],
      "P90": ["General", ["Visible", "Autowall", "Minimum", "Doubletap"],
          ["Visible", "Autowall", "Mindmg", "Doubletap"]
      ],
      "UMP45": ["General", ["Visible", "Autowall", "Minimum", "Doubletap"],
          ["Visible", "Autowall", "Mindmg", "Doubletap"]
      ],
      "MP5": ["General", ["Visible", "Autowall", "Minimum", "Doubletap"],
          ["Visible", "Autowall", "Mindmg", "Doubletap"]
      ],
      "MP7": ["General", ["Visible", "Autowall", "Minimum", "Doubletap"],
          ["Visible", "Autowall", "Mindmg", "Doubletap"]
      ],
      "Mac10": ["General", ["Visible", "Autowall", "Minimum", "Doubletap"],
          ["Visible", "Autowall", "Mindmg", "Doubletap"]
      ],
      "MP9": ["General", ["Visible", "Autowall", "Minimum", "Doubletap"],
          ["Visible", "Autowall", "Mindmg", "Doubletap"]
      ],
      "Deagle": ["Heavy pistol", ["Visible", "Autowall", "Minimum", "Doubletap"],
          ["Visible", "Autowall", "Mindmg", "Doubletap"]
      ],
      "Revolver": ["Heavy pistol", ["Visible", "Autowall", "Minimum"],
          ["Visible", "Autowall", "Mindmg"]
      ],
      "Five Seven": ["Pistol", ["Visible", "Autowall", "Minimum", "Doubletap"],
          ["Visible", "Autowall", "Mindmg", "Doubletap"]
      ],
      "Tec-9": ["Pistol", ["Visible", "Autowall", "Minimum", "Doubletap"],
          ["Visible", "Autowall", "Mindmg", "Doubletap"]
      ],
      "CZ-75": ["Pistol", ["Visible", "Autowall", "Minimum", "Doubletap"],
          ["Visible", "Autowall", "Mindmg", "Doubletap"]
      ],
      "P250": ["Pistol", ["Visible", "Autowall", "Minimum", "Doubletap"],
          ["Visible", "Autowall", "Mindmg", "Doubletap"]
      ],
      "Dualies": ["Pistol", ["Visible", "Autowall", "Minimum", "Doubletap"],
          ["Visible", "Autowall", "Mindmg", "Doubletap"]
      ],
      "Glock": ["Pistol", ["Visible", "Autowall", "Minimum", "Doubletap"],
          ["Visible", "Autowall", "Mindmg", "Doubletap"]
      ],
      "P2000": ["Pistol", ["Visible", "Autowall", "Minimum", "Doubletap"],
          ["Visible", "Autowall", "Mindmg", "Doubletap"]
      ],
      "USP": ["Pistol", ["Visible", "Autowall", "Minimum", "Doubletap"],
          ["Visible", "Autowall", "Mindmg", "Doubletap"]
      ]
  };
  var noScopeWeapons = ["General", "AUG", "SG553", "AUG", "AWP", "SSG08", "SCAR20", "G3SG1"];
  const weaponMenuItems = {
      ["Safe Point Override"]: {
          "type": 8,
          "default": 1
      },
      ["Body Aim Override"]: {
          "type": 8,
          "default": 1
      },
      ["Head Aim Override"]: {
          "type": 8,
          "default": 1
      },
      ["Minimum Damage Override"]: {
          "type": 8,
          "default": 1
      },
      ["Safe Point On"]: {
          "type": 3,
          "elements": ["Target Distance > X", "Target Crouching", "Target In-Air", "Missed X Shots", "Target Slow-Walking", "Target HP < X", "Target Distance <X"],
          "default": 0
      },
      ["Body Aim On"]: {
          "type": 3,
          "elements": ["Target Distance > X", "Target Crouching", "Target In-Air", "Missed X Shots", "Target Slow-Walking", "Target HP < X", "Target Distance <X"],
          "default": 0
      },
      ["Head Aim On"]: {
          "type": 3,
          "elements": ["Target Distance > X", "Target Crouching", "Target In-Air", "Missed X Shots", "Target Slow-Walking", "Target HP < X", "Target Distance <X"],
          "default": 0
      },
      ["Minimum Damage On"]: {
          "type": 3,
          "elements": ["Target Distance > X", "Target Crouching", "Target In-Air", "Missed X Shots", "Target Slow-Walking", "Target HP < X", "Target Distance <X"],
          "default": 0
      },
      ["Safe Point Distance > X"]: {
          "type": 7,
          "min": 0,
          "max": 4096,
          "default": 2048
      },
      ["Safe Point Distance < X"]: {
          "type": 7,
          "min": 0,
          "max": 4096,
          "default": 2048
      },
      ["Safe Point Misses > X"]: {
          "type": 7,
          "min": 0,
          "max": 10,
          "default": 2
      },
      ["Safe Point HP < X"]: {
          "type": 7,
          "min": 1,
          "max": 130,
          "default": 30
      },
      ["Body Aim Distance > X"]: {
          "type": 7,
          "min": 0,
          "max": 4096,
          "default": 2048
      },
      ["Body Aim Distance < X"]: {
          "type": 7,
          "min": 0,
          "max": 4096,
          "default": 2048
      },
      ["Body Aim Misses > X"]: {
          "type": 7,
          "min": 0,
          "max": 10,
          "default": 2
      },
      ["Body Aim HP < X"]: {
          "type": 7,
          "min": 1,
          "max": 130,
          "default": 30
      },
      ["Head Aim Distance > X"]: {
          "type": 7,
          "min": 0,
          "max": 4096,
          "default": 2048
      },
      ["Head Aim Distance < X"]: {
          "type": 7,
          "min": 0,
          "max": 4096,
          "default": 2048
      },
      ["Head Aim Misses > X"]: {
          "type": 7,
          "min": 0,
          "max": 10,
          "default": 2
      },
      ["Head Aim HP < X"]: {
          "type": 7,
          "min": 1,
          "max": 130,
          "default": 30
      },
      ["Minimum Damage Distance > X"]: {
          "type": 7,
          "min": 0,
          "max": 4096,
          "default": 2048
      },
      ["Minimum Damage Distance < X"]: {
          "type": 7,
          "min": 0,
          "max": 4096,
          "default": 2048
      },
      ["Minimum Damage Misses > X"]: {
          "type": 7,
          "min": 0,
          "max": 10,
          "default": 2
      },
      ["Minimum Damage HP < X"]: {
          "type": 7,
          "min": 1,
          "max": 130,
          "default": 30
      },
      ["Override Minimum Damage"]: {
          "type": 7,
          "min": 0,
          "max": 130,
          "default": 30
      }
  };
  //-----------------------------------------
  var playerMissed = {};
  var defaultWeaponsVisibility = 1;
  //-----------------------------------------
  var localPlayer = 0;
  var currentWeapon = "SSG08";
  var enemies = [0];
  var teammates = [0];
  var players = [0];
  var velocity = 0;
  var jump = 0;
  var duck = 0;
  var lastExploit = 0;
  var rageTarget = 0;
  //-----------------------------------------
  var espTime = {};
  var lastEspStatus = {};
  //-----------------------------------------
  var damageMode = "Idle";
  var accuracyMode = "Idle";
  var multipointMode = "RageAA";
  var hitboxMode = "Idle";
  //-----------------------------------------
  var playerWeaponFire = {};
  var shot = {};
  var hit = {};
  var damageList = [];
  //-----------------------------------------
  var antiAimMode = "Standing";
  var shotStart = {};
  var shotEnd = {};
  var onShotFire = 0;
  var closestEnemy = 0;
  //-----------------------------------------
  var enableFakeLag = true;
  var maxLevel = 25;
  var valve = false;
  //-----------------------------------------
  var forceMinimumDamageThisTick = false;
  //-----------------------------------------
  var swapBack = false;
  //-----------------------------------------
  var screen_size = Global.GetScreenSize();
  //----------------------------------------------------------------------------\\
  
  
  //----------------------------------------------------------------------------\\
  function getValue(key) {
      return UI.GetValue(["Config", "Weapon Config", "Weapon Config", key]);
  }
  
  function getColor(key) {
      return UI.GetColor(["Config", "Weapon Config", "Weapon Config", key]);
  }
  
  function setValue(key, value) {
      UI.SetValue(["Config", "Weapon Config", "Weapon Config",key], value);
  }
  
  function setColor(key, value) {
      UI.SetColor(["Config", "Weapon Config", "Weapon Config",key], value);
  }
  
  function setVisibility(key, value) {
      UI.SetEnabled(["Config", "Weapon Config", "Weapon Config",key], value);
  }
  function gethotkey(key){
      return UI.GetValue(["Rage", "General", "General", "Key assignment", key]);
  }
  //-----------------------------------------
  
  function getCurrentWeapon(player) {
      if (!Entity.IsAlive(player)) return "General";
      weapon = Entity.GetProp(player, "CBasePlayer", "m_hActiveWeapon");
      if (weapon == "m_hActiveWeapon") return "General";
      weapon = (Entity.GetProp(weapon, "CBaseAttributableItem", "m_iItemDefinitionIndex") & 0xFFFF);
      if (nameList[weapon] != undefined) {
          return nameList[weapon];
      } else {
          return "General";
      }
  }
  
  function getVelocity(index) {
      var velocity = Entity.GetProp(index, "CBasePlayer", "m_vecVelocity[0]");
      return Math.sqrt(velocity[0] * velocity[0] + velocity[1] * velocity[1]);
  }
  
  function getJump(index) {
      return Entity.GetProp(index, "CBasePlayer", "m_vecVelocity[2]")[0]
  }
  
  function getDuck(index) {
      return Entity.GetProp(index, "CCSPlayer", "m_flDuckAmount");
  }
  
  function getRandomInteger(min, max) {
      return min + Math.ceil(Math.random() * (max - min));
  }
  
  function getCurrentWeaponMenuValue(key) {
      return UI.GetValue(["Rage", "Accuracy", currentWeapon, key]);
  }
  
  function getHitboxName(index) {
      return hitboxes[index] || 'Generic';
  }
  
  function setAutoWallDisabled(on) {
      UI.SetValue(["Rage", "Target", "General", "Disable autowall"], on);
      UI.SetValue(["Rage", "Target", currentWeapon, "Disable autowall"], on);
  }
  //----------------------------------------------------------------------------\\
  
  function showDefaultWeapons(visibility) {
      if (visibility != defaultWeaponsVisibility) {
          allWeapons = UI.GetChildren(["Rage", "Target", "SHEET_MGR"]);
          for (i = 0; i < allWeapons.length; i++) {
              UI.SetEnabled(["Rage", "Target", allWeapons[i], "Field of view"], visibility);
              UI.SetEnabled(["Rage", "Target", allWeapons[i], "Minimum damage"], visibility);
              UI.SetEnabled(["Rage", "Target", allWeapons[i], "Disable autowall"], visibility);
              UI.SetEnabled(["Rage", "Target", allWeapons[i], "Hitboxes"], visibility);
              UI.SetEnabled(["Rage", "Target", allWeapons[i], "Multipoint hitboxes"], visibility);
              UI.SetEnabled(["Rage", "Target", allWeapons[i], "Head pointscale"], visibility);
              UI.SetEnabled(["Rage", "Target", allWeapons[i], "Body pointscale"], visibility);
              UI.SetEnabled(["Rage", "Accuracy", allWeapons[i], "Hitchance"], visibility);
          }
          UI.SetEnabled(["Rage", "Accuracy", "General", "Auto scope"], visibility);
          UI.SetEnabled(["Rage", "Accuracy", "AUG", "Auto scope"], visibility);
          UI.SetEnabled(["Rage", "Accuracy", "SG553", "Auto scope"], visibility);
          UI.SetEnabled(["Rage", "Accuracy", "AUG", "Auto scope"], visibility);
          UI.SetEnabled(["Rage", "Accuracy", "AWP", "Auto scope"], visibility);
          UI.SetEnabled(["Rage", "Accuracy", "SSG08", "Auto scope"], visibility);
          UI.SetEnabled(["Rage", "Accuracy", "SCAR20", "Auto scope"], visibility);
          UI.SetEnabled(["Rage", "Accuracy", "G3SG1", "Auto scope"], visibility);
          defaultWeaponsVisibility = visibility;
      }
  }
  
  function addWeaponMenuItems(weapon) {
      Object.keys(weaponMenuItems).forEach(function(key) {
          switch (weaponMenuItems[key]["type"]) {
              case 0:
                  UI.AddSubTab(["Rage", "Accuracy", weapon], key);
                  break;
              case 1:
                  UI.AddTextbox(["Rage", "Accuracy", weapon], key);
                  break;
              case 2:
                  UI.AddColorPicker(["Rage", "Accuracy", weapon], key);
                  break;
              case 3:
                  UI.AddMultiDropdown(["Rage", "Accuracy", weapon], key, weaponMenuItems[key]["elements"]);
                  break;
              case 4:
                  UI.AddDropdown(["Rage", "Accuracy", weapon], key, weaponMenuItems[key]["elements"], weaponMenuItems[key]["searchbar"]);
                  break;
              case 5:
                  UI.AddHotkey(["Rage", "Accuracy", weapon], key, weaponMenuItems[key]["short"]);
                  break;
              case 6:
                  UI.AddSliderFloat(["Rage", "Accuracy", weapon], key, weaponMenuItems[key]["min"], weaponMenuItems[key]["max"]);
                  break;
              case 7:
                  UI.AddSliderInt(["Rage", "Accuracy", weapon], key, weaponMenuItems[key]["min"], weaponMenuItems[key]["max"]);
                  break;
              case 8:
                  UI.AddCheckbox(["Rage", "Accuracy", weapon], key);
                  break;
              case 9:
                  UI.AddSliderInt(["Rage", "Accuracy", weapon], key, 0, 0);
                  break;
          }
          UI.SetEnabled(["Rage", "Accuracy", weapon, key], 0);
      });
  }
  
  
  function addWeapons() {
      allWeapons = UI.GetChildren(["Rage", "Target", "SHEET_MGR"]);
      for (x = 0; x < allWeapons.length; x++) {
          UI.AddDropdown(["Rage", "Target", allWeapons[x]], "Mode", weaponSettings[allWeapons[x]][1], 0);
          for (i = 0; i < weaponSettings[allWeapons[x]][1].length; i++) {
              UI.AddSliderInt(["Rage", "Target", allWeapons[x]], weaponSettings[allWeapons[x]][1][i] + " Damage", 0, 130);
              UI.SetEnabled(["Rage", "Target", allWeapons[x], weaponSettings[allWeapons[x]][1][i] + " Damage"], 0);
              UI.AddSliderInt(["Rage", "Target", allWeapons[x]], weaponSettings[allWeapons[x]][1][i] + " Hitchance", 0, 100);
              UI.SetEnabled(["Rage", "Target", allWeapons[x], weaponSettings[allWeapons[x]][1][i] + " Hitchance"], 0);
          }
  
          for (i = 0; i < weaponSettings[allWeapons[x]][2].length; i++) {
              UI.AddMultiDropdown(["Rage", "Target", allWeapons[x]], weaponSettings[allWeapons[x]][2][i] + " Hitboxes", ["Head", "Upper Chest", "Chest", "Lower Chest", "Stomach", "Pelvis", "Legs", "Feet", "Arms"]);
              UI.SetEnabled(["Rage", "Target", allWeapons[x], weaponSettings[allWeapons[x]][2][i] + " Hitboxes"], 0);
          }
  
          for (i = 0; i < weaponSettings[allWeapons[x]][2].length; i++) {
              UI.AddMultiDropdown(["Rage", "Target", allWeapons[x]], weaponSettings[allWeapons[x]][2][i] + " Multipoint Hitboxes", ["Head", "Upper Chest", "Chest", "Lower Chest", "Stomach", "Pelvis", "Legs", "Feet", "Arms"]);
              UI.SetEnabled(["Rage", "Target", allWeapons[x], weaponSettings[allWeapons[x]][2][i] + " Multipoint Hitboxes"], 0);
          }
  
          UI.AddDropdown(["Rage", "Target", allWeapons[x]], "Enemy Anti-Aim", ["LegitAA", "RageAA"], 0);
          UI.AddSliderInt(["Rage", "Target", allWeapons[x]], "LegitAA Head Point Scale", 0, 100);
          UI.AddSliderInt(["Rage", "Target", allWeapons[x]], "LegitAA Body Point Scale", 0, 100);
          UI.AddSliderInt(["Rage", "Target", allWeapons[x]], "RageAA Head Point Scale", 0, 100);
          UI.AddSliderInt(["Rage", "Target", allWeapons[x]], "RageAA Body Point Scale", 0, 100);
          UI.SetEnabled(["Rage", "Target", allWeapons[x], "LegitAA Head Point Scale"], 0);
          UI.SetEnabled(["Rage", "Target", allWeapons[x], "LegitAA Body Point Scale"], 0);
          UI.SetEnabled(["Rage", "Target", allWeapons[x], "RageAA Head Point Scale"], 0);
          UI.SetEnabled(["Rage", "Target", allWeapons[x], "RageAA Body Point Scale"], 0);
          if (noScopeWeapons.indexOf(allWeapons[x]) != -1) {
              UI.AddSliderInt(["Rage", "Target", allWeapons[x]], "No Scope Distance", 0, 2048);
              UI.SetEnabled(["Rage", "Target", allWeapons[x], "No Scope Distance"], 0);
          }
          addWeaponMenuItems(allWeapons[x]);
      }
  }
  
  function hideWeapons() {
      allWeapons = UI.GetChildren(["Rage", "Target", "SHEET_MGR"]);
      for (x = 0; x < allWeapons.length; x++) {
          for (i = 0; i < weaponSettings[allWeapons[x]][1].length; i++) {
              UI.SetEnabled(["Rage", "Target", allWeapons[x], weaponSettings[allWeapons[x]][1][i] + " Damage"], 0);
              UI.SetEnabled(["Rage", "Target", allWeapons[x], weaponSettings[allWeapons[x]][1][i] + " Hitchance"], 0);
          }
  
          for (i = 0; i < weaponSettings[allWeapons[x]][2].length; i++) {
              UI.SetEnabled(["Rage", "Target", allWeapons[x], weaponSettings[allWeapons[x]][2][i] + " Hitboxes"], 0);
              UI.SetEnabled(["Rage", "Target", allWeapons[x], weaponSettings[allWeapons[x]][2][i] + " Multipoint Hitboxes"], 0);
          }
  
          UI.SetEnabled(["Rage", "Target", allWeapons[x], "Mode"], 0);
          UI.SetEnabled(["Rage", "Target", allWeapons[x], "Enemy Anti-Aim"], 0);
          UI.SetEnabled(["Rage", "Target", allWeapons[x], "LegitAA Head Point Scale"], 0);
          UI.SetEnabled(["Rage", "Target", allWeapons[x], "LegitAA Body Point Scale"], 0);
          UI.SetEnabled(["Rage", "Target", allWeapons[x], "RageAA Head Point Scale"], 0);
          UI.SetEnabled(["Rage", "Target", allWeapons[x], "RageAA Body Point Scale"], 0);
          if (noScopeWeapons.indexOf(allWeapons[x]) != -1) {
              UI.SetEnabled(["Rage", "Target", allWeapons[x], "No Scope Distance"], 0);
          }
          Object.keys(weaponMenuItems).forEach(function(key) {
              if (weaponMenuItems[key]["type"] != 0) {
                  UI.SetEnabled(["Rage", "Accuracy", allWeapons[x], key], 0);
              }
          });
      }
  }
  
  function showActiveItems() {
      setVisibility("Enable Weapon Config", 1);
      setVisibility("Enable Rage Optimization", 1);
      if (getValue("Enable Weapon Config")) {
          showDefaultWeapons(0);
          setVisibility(">>-PASTED Weapon Config -<<", 1);
          setVisibility("Automatic Mindmg", 1);
          if (getValue("Automatic Mindmg") == 1) {
              setVisibility("Automatic Mindmg Offset", 1);
          }else{
              setVisibility("Automatic Mindmg Offset", 0);
          }
          allWeapons = UI.GetChildren(["Rage", "Target", "SHEET_MGR"]);
          for (x = 0; x < allWeapons.length; x++) {
              UI.SetEnabled(["Rage", "Target", allWeapons[x], "Mode"], 1);
              UI.SetEnabled(["Rage", "Target", allWeapons[x], "Enemy Anti-Aim"], 1);
              if (UI.GetString(["Rage", "Target", allWeapons[x], "Mode"]) != "...") {
                  UI.SetEnabled(["Rage", "Target", allWeapons[x], UI.GetString(["Rage", "Target", allWeapons[x], "Mode"]) + " Damage"], 1);
                  UI.SetEnabled(["Rage", "Target", allWeapons[x], UI.GetString(["Rage", "Target", allWeapons[x], "Mode"]) + " Hitchance"], 1);
                  hitboxType = (UI.GetString(["Rage", "Target", allWeapons[x], "Mode"]) == "Minimum") ? "Mindmg" : UI.GetString(["Rage", "Target", allWeapons[x], "Mode"]);
                  UI.SetEnabled(["Rage", "Target", allWeapons[x], hitboxType + " Hitboxes"], 1);
                  UI.SetEnabled(["Rage", "Target", allWeapons[x], hitboxType + " Multipoint Hitboxes"], 1);
              }
              if (UI.GetString(["Rage", "Target", allWeapons[x], "Enemy Anti-Aim"]) != "...") {
                  UI.SetEnabled(["Rage", "Target", allWeapons[x], UI.GetString(["Rage", "Target", allWeapons[x], "Enemy Anti-Aim"]) + " Head Point Scale"], 1);
                  UI.SetEnabled(["Rage", "Target", allWeapons[x], UI.GetString(["Rage", "Target", allWeapons[x], "Enemy Anti-Aim"]) + " Body Point Scale"], 1);
              }
              if (noScopeWeapons.indexOf(allWeapons[x]) != -1) {
                  UI.SetEnabled(["Rage", "Target", allWeapons[x], "No Scope Distance"], 1);
              }
          }
  
      } else {
          showDefaultWeapons(1);
          setVisibility(">>-PASTED Weapon Config -<<", 0);
          setVisibility("Automatic Mindmg", 0);
          setVisibility("Automatic Mindmg Offset", 0);
      }
      if (getValue("Enable Rage Optimization")) {
          setVisibility(">>-PASTED Rage Optimization -<<", 1);
          setVisibility("Teleport", 1);
          allWeapons = UI.GetChildren(["Rage", "Accuracy", "SHEET_MGR"]);
          for (x = 0; x < allWeapons.length; x++) {
              UI.SetEnabled(["Rage", "Accuracy", allWeapons[x], "Safe Point Override"], 1);
              UI.SetEnabled(["Rage", "Accuracy", allWeapons[x], "Body Aim Override"], 1);
              UI.SetEnabled(["Rage", "Accuracy", allWeapons[x], "Head Aim Override"], 1);
              UI.SetEnabled(["Rage", "Accuracy", allWeapons[x], "Minimum Damage Override"], 1);
              if (UI.GetValue(["Rage", "Accuracy", allWeapons[x], "Safe Point Override"])) {
                  UI.SetEnabled(["Rage", "Accuracy", allWeapons[x], "Safe Point On"], 1);
                  if (UI.GetValue(["Rage", "Accuracy", allWeapons[x], "Safe Point On"]) & (1 << 0)) {
                      UI.SetEnabled(["Rage", "Accuracy", allWeapons[x], "Safe Point Distance > X"], 1);
                  }
                  if (UI.GetValue(["Rage", "Accuracy", allWeapons[x], "Safe Point On"]) & (1 << 3)) {
                      UI.SetEnabled(["Rage", "Accuracy", allWeapons[x], "Safe Point Misses > X"], 1);
                  }
                  if (UI.GetValue(["Rage", "Accuracy", allWeapons[x], "Safe Point On"]) & (1 << 5)) {
                      UI.SetEnabled(["Rage", "Accuracy", allWeapons[x], "Safe Point HP < X"], 1);
                  }
                  if (UI.GetValue(["Rage", "Accuracy", allWeapons[x], "Safe Point On"]) & (1 << 6)) {
                      UI.SetEnabled(["Rage", "Accuracy", allWeapons[x], "Safe Point Distance < X"], 1);
                  }
              }
              if (UI.GetValue(["Rage", "Accuracy", allWeapons[x], "Body Aim Override"])) {
                  UI.SetEnabled(["Rage", "Accuracy", allWeapons[x], "Body Aim On"], 1);
                  if (UI.GetValue(["Rage", "Accuracy", allWeapons[x], "Body Aim On"]) & (1 << 0)) {
                      UI.SetEnabled(["Rage", "Accuracy", allWeapons[x], "Body Aim Distance > X"], 1);
                  }
                  if (UI.GetValue(["Rage", "Accuracy", allWeapons[x], "Body Aim On"]) & (1 << 3)) {
                      UI.SetEnabled(["Rage", "Accuracy", allWeapons[x], "Body Aim Misses > X"], 1);
                  }
                  if (UI.GetValue(["Rage", "Accuracy", allWeapons[x], "Body Aim On"]) & (1 << 5)) {
                      UI.SetEnabled(["Rage", "Accuracy", allWeapons[x], "Body Aim HP < X"], 1);
                  }
                  if (UI.GetValue(["Rage", "Accuracy", allWeapons[x], "Body Aim On"]) & (1 << 6)) {
                      UI.SetEnabled(["Rage", "Accuracy", allWeapons[x], "Body Aim Distance < X"], 1);
                  }
              }
              if (UI.GetValue(["Rage", "Accuracy", allWeapons[x], "Head Aim Override"])) {
                  UI.SetEnabled(["Rage", "Accuracy", allWeapons[x], "Head Aim On"], 1);
                  if (UI.GetValue(["Rage", "Accuracy", allWeapons[x], "Head Aim On"]) & (1 << 0)) {
                      UI.SetEnabled(["Rage", "Accuracy", allWeapons[x], "Head Aim Distance > X"], 1);
                  }
                  if (UI.GetValue(["Rage", "Accuracy", allWeapons[x], "Head Aim On"]) & (1 << 3)) {
                      UI.SetEnabled(["Rage", "Accuracy", allWeapons[x], "Head Aim Misses > X"], 1);
                  }
                  if (UI.GetValue(["Rage", "Accuracy", allWeapons[x], "Head Aim On"]) & (1 << 5)) {
                      UI.SetEnabled(["Rage", "Accuracy", allWeapons[x], "Head Aim HP < X"], 1);
                  }
                  if (UI.GetValue(["Rage", "Accuracy", allWeapons[x], "Head Aim On"]) & (1 << 6)) {
                      UI.SetEnabled(["Rage", "Accuracy", allWeapons[x], "Head Aim Distance < X"], 1);
                  }
              }
              if (UI.GetValue(["Rage", "Accuracy", allWeapons[x], "Minimum Damage Override"])) {
                  UI.SetEnabled(["Rage", "Accuracy", allWeapons[x], "Minimum Damage On"], 1);
                  if (UI.GetValue(["Rage", "Accuracy", allWeapons[x], "Minimum Damage On"]) & (1 << 0)) {
                      UI.SetEnabled(["Rage", "Accuracy", allWeapons[x], "Minimum Damage Distance > X"], 1);
                  }
                  if (UI.GetValue(["Rage", "Accuracy", allWeapons[x], "Minimum Damage On"]) & (1 << 3)) {
                      UI.SetEnabled(["Rage", "Accuracy", allWeapons[x], "Minimum Damage Misses > X"], 1);
                  }
                  if (UI.GetValue(["Rage", "Accuracy", allWeapons[x], "Minimum Damage On"]) & (1 << 5)) {
                      UI.SetEnabled(["Rage", "Accuracy", allWeapons[x], "Minimum Damage HP < X"], 1);
                  }
                  if (UI.GetValue(["Rage", "Accuracy", allWeapons[x], "Minimum Damage On"]) & (1 << 6)) {
                      UI.SetEnabled(["Rage", "Accuracy", allWeapons[x], "Minimum Damage Distance < X"], 1);
                  }
                  UI.SetEnabled(["Rage", "Accuracy", allWeapons[x], "Override Minimum Damage"], 1);
              }
          }
      }else{
          setVisibility(">>-PASTED Rage Optimization -<<", 0);
          setVisibility("Teleport", 0);
      }
  }
  
  function hideAllItems() {
      hideWeapons();
  }
  
  function initializeMenuItems() {
      UI.SetValue(["Cheat", "General", "Restrictions"], 0);
      addWeapons();
      hideAllItems();
  }
  
  function Weapon_onCreateMove() {
  
      cacheValues();
      weaponConfigUpdate();
      rageBotUpdate();
  }
  
  initializeMenuItems();
  
  //----------------------------------------------------------------------------\\
  
  function calcClosestEnemy() {
      if (!Entity.IsAlive(closestEnemy)) {
          closestEnemy = 0;
      }
      closestDistance = Math.sqrt(Math.pow(screen_size[0] / 2, 2) + Math.pow(screen_size[1] / 2, 2)) / 2;
      closestGuy = 0;
      for (i = 0; i < enemies.length; i++) {
          enmiScreenPos = Render.WorldToScreen(Entity.GetEyePosition(enemies[i]));
          if (enmiScreenPos != undefined) {
              thisGuysDistance = Math.sqrt(Math.pow(Math.abs(Math.abs(enmiScreenPos[0]) - screen_size[0] / 2), 2) + Math.pow(Math.abs(Math.abs(enmiScreenPos[1]) - screen_size[1] / 2), 2));
              if (thisGuysDistance < closestDistance) {
                  closestDistance = thisGuysDistance;
                  closestGuy = enemies[i];
              }
          }
      }
      if (closestEnemy != closestGuy && closestGuy != 0) {
          closestEnemy = closestGuy;
          closestEnemyChanged = true;
      }
  }
  function cacheValues() {
      target = Ragebot.GetTarget();
      calcClosestEnemy();
      if (target != 0) {
          rageTarget = target;
      }
      if (!Entity.IsAlive(rageTarget) || Entity.IsDormant(rageTarget)) {
          rageTarget = 0;
      }
      if (rageTarget == 0 && closestEnemy != 0) {
          rageTarget = closestEnemy;
      }
      localPlayer = Entity.GetLocalPlayer();
      enemies = Entity.GetEnemies();
      teammates = Entity.GetTeammates();
      players = Entity.GetPlayers();
      velocity = getVelocity(localPlayer);
      jump = getJump(localPlayer);
      duck = getDuck(localPlayer);
      currentWeapon = getCurrentWeapon(localPlayer);
  }
  
  function onWeaponFire() {
      if (Entity.GetEntityFromUserID(Event.GetInt("userid")) == localPlayer) {
          onShotFire = 8;
      }
  if (getValue("Enable Weapon Config") == 1) {
      playerWeaponFire[Entity.GetEntityFromUserID(Event.GetInt("userid"))] = Globals.Tickcount();
  }
  if (Entity.IsLocalPlayer(Entity.GetEntityFromUserID(Event.GetInt("userid")))) {
      if (shot[currentWeapon] == undefined) {
          shot[currentWeapon] = 1;
      } else {
          shot[currentWeapon]++;
      }
  }
  }
  
  function ignoreTargetInSmoke() {
      targets = Entity.GetEnemies();
      for (i = 0; i < targets.length; i++) {
          if (Trace.Smoke(Entity.GetEyePosition(localPlayer), Entity.GetHitboxPosition(targets[i], 0)) == 1) {
              Ragebot.IgnoreTarget(targets[i]);
          }
      }
  }
  
  function ignoreIfCannotSee() {
      penetrable = 0.99;
      ignoreList = [];
      localEyePos = Entity.GetEyePosition(localPlayer);
      for (i = 0; i < ignoreList.length; i++) {
          Ragebot.IgnoreTarget(ignoreList[i]);
      }
      setAutoWallDisabled(0);
  }
  
  //----------------------------------------------------------------------------\\
  
  function noScopeUpdate() {
      if (noScopeWeapons.indexOf(currentWeapon) != -1 && Entity.IsAlive(localPlayer)) {
          distance = 0;
          for (i = 0; i < enemies.length; i++) {
              if (Entity.IsAlive(enemies[i]) && !Entity.IsDormant(enemies[i])) {
                  origin = Entity.GetRenderOrigin(enemies[i]);
                  myself = Entity.GetRenderOrigin(localPlayer);
                  distance_to_enemy = Math.sqrt(Math.pow(origin[0] - myself[0], 2) + Math.pow(origin[1] - myself[1], 2) + Math.pow(origin[2] - myself[2], 2));
                  if (distance == 0 || distance_to_enemy < distance) {
                      distance = distance_to_enemy;
                  }
              }
          }
          if (distance < UI.GetValue(["Rage", "Target", currentWeapon, "No Scope Distance"]) && distance != 0) {
              UI.SetValue(["Rage", "Accuracy", "General", "Auto scope"], 0);
              UI.SetValue(["Rage", "Accuracy", currentWeapon, "Auto scope"], 0);
          } else {
              UI.SetValue(["Rage", "Accuracy", "General", "Auto scope"], 1);
              UI.SetValue(["Rage", "Accuracy", currentWeapon, "Auto scope"], 1);
          }
      }
  }
  
  function weaponConfigUpdate() {
      if (getValue("Enable Weapon Config")) {
          weaponDamageUpdate();
          weaponAccuracyUpdate();
          weaponMultipointUpdate();
          noScopeUpdate();
      }
  }
  
  function weaponMultipointUpdate() {
      if (Entity.IsAlive(rageTarget) && !Entity.IsDormant(rageTarget)) {
          targetAngle = Entity.GetProp(rageTarget, "CCSPlayer", "m_angEyeAngles[0]")[0];
          if (targetAngle > 75 && targetAngle <= 90) {
              multipointMode = "RageAA";
              UI.SetValue(["Rage", "Target", "General", "Head pointscale"], UI.GetValue(["Rage", "Target", currentWeapon, "RageAA Head Point Scale"]));
              UI.SetValue(["Rage", "Target", currentWeapon, "Head pointscale"], UI.GetValue(["Rage", "Target", currentWeapon, "RageAA Head Point Scale"]));
              UI.SetValue(["Rage", "Target", "General", "Body pointscale"], UI.GetValue(["Rage", "Target", currentWeapon, "RageAA Body Point Scale"]));
              UI.SetValue(["Rage", "Target", currentWeapon, "Body pointscale"], UI.GetValue(["Rage", "Target", currentWeapon, "RageAA Body Point Scale"]));
          } else {
              multipointMode = "LegitAA";
              UI.SetValue(["Rage", "Target", "General", "Head pointscale"], UI.GetValue(["Rage", "Target", currentWeapon, "LegitAA Head Point Scale"]));
              UI.SetValue(["Rage", "Target", currentWeapon, "Head pointscale"], UI.GetValue(["Rage", "Target", currentWeapon, "LegitAA Head Point Scale"]));
              UI.SetValue(["Rage", "Target", "General", "Body pointscale"], UI.GetValue(["Rage", "Target", currentWeapon, "LegitAA Body Point Scale"]));
              UI.SetValue(["Rage", "Target", currentWeapon, "Body pointscale"], UI.GetValue(["Rage", "Target", currentWeapon, "LegitAA Body Point Scale"]));
          }
      } else {
          multipointMode = "RageAA";
          UI.SetValue(["Rage", "Target", "General", "Head pointscale"], UI.GetValue(["Rage", "Target", currentWeapon, "RageAA Head Point Scale"]));
          UI.SetValue(["Rage", "Target", currentWeapon, "Head pointscale"], UI.GetValue(["Rage", "Target", currentWeapon, "RageAA Head Point Scale"]));
          UI.SetValue(["Rage", "Target", "General", "Body pointscale"], UI.GetValue(["Rage", "Target", currentWeapon, "RageAA Body Point Scale"]));
          UI.SetValue(["Rage", "Target", currentWeapon, "Body pointscale"], UI.GetValue(["Rage", "Target", currentWeapon, "RageAA Body Point Scale"]));
      }
  }
  
  function weaponAccuracyUpdate() {
      if (gethotkey("Minimum accuracy")) {
          setAccuracyMode("Minimum");
          return;
      }
  /*     if (getJump(localPlayer) != 0) {
          setAccuracyMode("Minimum");
          accuracyMode = "Air Minimum";
          return;
      } */
      if (noScopeWeapons.indexOf(currentWeapon) != -1 && !UI.GetValue(["Rage", "Accuracy", "General", "Auto scope"]) && Entity.GetProp(localPlayer, "CCSPlayer", "m_bIsScoped") == false) {
          setAccuracyMode("Minimum");
          accuracyMode = "No Scope";
          return;
      }
      if (UI.GetValue(["Rage", "Exploits", "Keys", "Key assignment", "Double tap"]) && (Exploit.GetCharge() == 1.0 || lastExploit == 1) && weaponSettings[currentWeapon][1].indexOf("Doubletap") != -1) {
          setAccuracyMode("Doubletap");
          return;
      }
      if (Entity.IsValid(rageTarget) == true && Entity.IsAlive(rageTarget) && Entity.IsDormant(rageTarget) == false) {
          localPlayer_index = localPlayer;
          localPlayer_eyepos = Entity.GetEyePosition(localPlayer_index);
          hitbox_pos = Entity.GetHitboxPosition(rageTarget, 0);
          result = Trace.Bullet(localPlayer_index, rageTarget, localPlayer_eyepos, hitbox_pos);
          if (result[2]) {
              setAccuracyMode("Visible");
          } else {
              setAccuracyMode("Autowall");
          }
      } else {
          setAccuracyMode("Visible");
      }
  }
  
  function weaponDamageUpdate() {
      if (gethotkey("Minimum damage") || forceMinimumDamageThisTick) {
          setDamageMode("Minimum");
          setHitboxes("Mindmg");
          forceMinimumDamageThisTick = false;
          return;
      }
      if (UI.GetValue(["Rage", "Exploits", "Keys", "Key assignment", "Double tap"]) && (Exploit.GetCharge() == 1.0 || lastExploit == 1) && weaponSettings[currentWeapon][1].indexOf("Doubletap") != -1) {
          setDamageMode("Doubletap");
          setHitboxes("Doubletap");
          if (getValue("Automatic Mindmg")) {
              if (Exploit.GetCharge() == 1.0) {
                  if (Entity.GetProp(rageTarget, "CBasePlayer", "m_iHealth") < (UI.GetValue(["Rage", "Target", currentWeapon, "Minimum damage"]) * 2) && Entity.GetProp(rageTarget, "CBasePlayer", "m_iHealth") > 0 && UI.GetValue(["Rage", "Target", currentWeapon, "Minimum damage"]) < 101) {
                      UI.SetValue(["Rage", "Target", currentWeapon, "Minimum damage"], (Entity.GetProp(rageTarget, "CBasePlayer", "m_iHealth") / 2) + getValue("Automatic Mindmg Offset"));
                      UI.SetValue(["Rage", "Target", "General", "Minimum damage"], (Entity.GetProp(rageTarget, "CBasePlayer", "m_iHealth") / 2) + getValue("Automatic Mindmg Offset"));
                      damageMode = "Auto Doubletap";
                  }
              } else {
                  if (Entity.GetProp(rageTarget, "CBasePlayer", "m_iHealth") < UI.GetValue(["Rage", "Target", currentWeapon, "Minimum damage"]) && Entity.GetProp(rageTarget, "CBasePlayer", "m_iHealth") > 0 && UI.GetValue(["Rage", "Target", currentWeapon, "Minimum damage"]) < 101) {
                      UI.SetValue(["Rage", "Target", currentWeapon, "Minimum damage"], Entity.GetProp(rageTarget, "CBasePlayer", "m_iHealth") + getValue("Automatic Mindmg Offset"));
                      UI.SetValue(["Rage", "Target", "General", "Minimum damage"], Entity.GetProp(rageTarget, "CBasePlayer", "m_iHealth") + getValue("Automatic Mindmg Offset"));
                      damageMode = "Auto";
                  }
              }
          }
          return;
      }
      visHitboxes = UI.GetValue(["Rage", "Target", currentWeapon, "Visible Hitboxes"]);
      hidHitboxes = UI.GetValue(["Rage", "Target", currentWeapon, "Autowall Hitboxes"]);
      visMultiHitboxes = UI.GetValue(["Rage", "Target", currentWeapon, "Visible Multipoint Hitboxes"]);
      hidMultiHitboxes = UI.GetValue(["Rage", "Target", currentWeapon, "Autowall Multipoint Hitboxes"]);
      visDamage = UI.GetValue(["Rage", "Target", currentWeapon, "Visible Damage"]);
      hidDamage = UI.GetValue(["Rage", "Target", currentWeapon, "Autowall Damage"]);
      if (Entity.IsValid(rageTarget) == true && Entity.IsAlive(rageTarget) && Entity.IsDormant(rageTarget) == false) {
          localPlayer_index = localPlayer;
          localPlayer_eyepos = Entity.GetEyePosition(localPlayer_index);
          visibleList = [];
          hiddenList = [];
          for (x = 0; x < 13; x++) {
              hitboxPos = Entity.GetHitboxPosition(rageTarget, x);
              result = Trace.Bullet(localPlayer_index, rageTarget, localPlayer_eyepos, hitboxPos);
              if (result[2]) {
                  switch (x) {
                      case 0:
                          if (visHitboxes & (1 << 0) || visMultiHitboxes & (1 << 0)) {
                              visibleList.push(result[1]);
                          }
                          break;
                      case 1:
                          if (visHitboxes & (1 << 0) || visMultiHitboxes & (1 << 0)) {
                              visibleList.push(result[1]);
                          }
                          break;
                      case 2:
                          if (visHitboxes & (1 << 5) || visMultiHitboxes & (1 << 5)) {
                              visibleList.push(result[1]);
                          }
                          break;
                      case 3:
                          if (visHitboxes & (1 << 1) || visHitboxes & (1 << 2) || visHitboxes & (1 << 3) || visHitboxes & (1 << 4) || visMultiHitboxes & (1 << 1) || visMultiHitboxes & (1 << 2) || visMultiHitboxes & (1 << 3) || visMultiHitboxes & (1 << 4)) {
                              visibleList.push(result[1]);
                          }
                          break;
                      case 4:
                          if (visHitboxes & (1 << 1) || visHitboxes & (1 << 2) || visHitboxes & (1 << 3) || visMultiHitboxes & (1 << 1) || visMultiHitboxes & (1 << 2) || visMultiHitboxes & (1 << 3)) {
                              visibleList.push(result[1]);
                          }
                          break;
                      case 5:
                          if (visHitboxes & (1 << 2) || visMultiHitboxes & (1 << 2)) {
                              visibleList.push(result[1]);
                          }
                          break;
                      case 6:
                          if (visHitboxes & (1 << 1) || visMultiHitboxes & (1 << 1)) {
                              visibleList.push(result[1]);
                          }
                          break;
                      case 7:
                          if (visHitboxes & (1 << 6) || visMultiHitboxes & (1 << 6)) {
                              visibleList.push(result[1]);
                          }
                          break;
                      case 8:
                          if (visHitboxes & (1 << 6) || visMultiHitboxes & (1 << 6)) {
                              visibleList.push(result[1]);
                          }
                          break;
                      case 9:
                          if (visHitboxes & (1 << 6) || visMultiHitboxes & (1 << 6)) {
                              visibleList.push(result[1]);
                          }
                          break;
                      case 10:
                          if (visHitboxes & (1 << 6) || visMultiHitboxes & (1 << 6)) {
                              visibleList.push(result[1]);
                          }
                          break;
                      case 11:
                          if (visHitboxes & (1 << 7) || visMultiHitboxes & (1 << 7)) {
                              visibleList.push(result[1]);
                          }
                          break;
                      case 12:
                          if (visHitboxes & (1 << 7) || visMultiHitboxes & (1 << 7)) {
                              visibleList.push(result[1]);
                          }
                          break;
                  }
              } else {
                  switch (x) {
                      case 0:
                          if (hidHitboxes & (1 << 0) || hidMultiHitboxes & (1 << 0)) {
                              hiddenList.push(result[1]);
                          }
                          break;
                      case 1:
                          if (hidHitboxes & (1 << 0) || hidMultiHitboxes & (1 << 0)) {
                              hiddenList.push(result[1]);
                          }
                          break;
                      case 2:
                          if (hidHitboxes & (1 << 5) || hidMultiHitboxes & (1 << 5)) {
                              hiddenList.push(result[1]);
                          }
                          break;
                      case 3:
                          if (hidHitboxes & (1 << 1) || hidHitboxes & (1 << 2) || hidHitboxes & (1 << 3) || hidHitboxes & (1 << 4) || hidMultiHitboxes & (1 << 1) || hidMultiHitboxes & (1 << 2) || hidMultiHitboxes & (1 << 3) || hidMultiHitboxes & (1 << 4)) {
                              hiddenList.push(result[1]);
                          }
                          break;
                      case 4:
                          if (hidHitboxes & (1 << 1) || hidHitboxes & (1 << 2) || hidHitboxes & (1 << 3) || hidMultiHitboxes & (1 << 1) || hidMultiHitboxes & (1 << 2) || hidMultiHitboxes & (1 << 3)) {
                              hiddenList.push(result[1]);
                          }
                          break;
                      case 5:
                          if (hidHitboxes & (1 << 2) || hidMultiHitboxes & (1 << 2)) {
                              hiddenList.push(result[1]);
                          }
                          break;
                      case 6:
                          if (hidHitboxes & (1 << 1) || hidMultiHitboxes & (1 << 1)) {
                              hiddenList.push(result[1]);
                          }
                          break;
                      case 7:
                          if (hidHitboxes & (1 << 6) || hidMultiHitboxes & (1 << 6)) {
                              hiddenList.push(result[1]);
                          }
                          break;
                      case 8:
                          if (hidHitboxes & (1 << 6) || hidMultiHitboxes & (1 << 6)) {
                              hiddenList.push(result[1]);
                          }
                          break;
                      case 9:
                          if (hidHitboxes & (1 << 6) || hidMultiHitboxes & (1 << 6)) {
                              hiddenList.push(result[1]);
                          }
                          break;
                      case 10:
                          if (hidHitboxes & (1 << 6) || hidMultiHitboxes & (1 << 6)) {
                              hiddenList.push(result[1]);
                          }
                          break;
                      case 11:
                          if (hidHitboxes & (1 << 7) || hidMultiHitboxes & (1 << 7)) {
                              hiddenList.push(result[1]);
                          }
                          break;
                      case 12:
                          if (hidHitboxes & (1 << 7) || hidMultiHitboxes & (1 << 7)) {
                              hiddenList.push(result[1]);
                          }
                          break;
                  }
              }
          }
          visibleDamage = Math.max.apply(null, visibleList);
          hiddenDamage = Math.max.apply(null, hiddenList);
          if (visibleDamage < 0) {
              visibleDamage = 0;
          }
          if (hiddenDamage < 0) {
              hiddenDamage = 0;
          }
          if (visibleDamage > visDamage) {
              if (hiddenDamage > hidDamage) {
                  if ((visibleDamage - visDamage) > (hiddenDamage - hidDamage)) {
                      setDamageMode("Visible");
                      setHitboxes("Visible");
                  } else {
                      setDamageMode("Autowall");
                      setHitboxes("Autowall");
                  }
              } else {
                  setDamageMode("Visible");
                  setHitboxes("Visible");
              }
          } else {
              setDamageMode("Autowall");
              setHitboxes("Autowall");
          }
          if (getValue("Automatic Mindmg")) {
              if (Entity.GetProp(rageTarget, "CBasePlayer", "m_iHealth") < UI.GetValue(["Rage", "Target", currentWeapon, "Minimum damage"]) && Entity.GetProp(rageTarget, "CBasePlayer", "m_iHealth") > 0 && UI.GetValue(["Rage", "Target", currentWeapon, "Minimum damage"]) < 101) {
                  UI.SetValue(["Rage", "Target", currentWeapon, "Minimum damage"], Entity.GetProp(rageTarget, "CBasePlayer", "m_iHealth") + getValue("Automatic Mindmg Offset"));
                  UI.SetValue(["Rage", "Target", "General", "Minimum damage"], Entity.GetProp(rageTarget, "CBasePlayer", "m_iHealth") + getValue("Automatic Mindmg Offset"));
                  damageMode = "Auto";
              }
          }
      } else {
          if (visDamage > hidDamage) {
              setDamageMode("Autowall");
          } else {
              setDamageMode("Visible");
          }
          setHitboxes("Idle");
      }
  }
  
  function rageBotUpdate() {
      if (getValue("Enable Rage Optimization") == 1) {
          if (getValue("Teleport") == 1) {
              weapon = Entity.GetProp(localPlayer, "CBasePlayer", "m_hActiveWeapon");
              weapon = (Entity.GetProp(weapon, "CBaseAttributableItem", "m_iItemDefinitionIndex") & 0xFFFF);
              nades = [43, 44, 45, 47, 48];
              if (nades.indexOf(weapon) == -1) {
                  if (onShotFire > 0 && onShotFire < 13) {
                      setHideShots(0);
                  } else {
                      setHideShots(1);
                  }
              }
          }
          if (getCurrentWeaponMenuValue("Safe Point Override") == 1) {
              safepointUpdate();
          }
          if (getCurrentWeaponMenuValue("Body Aim Override") == 1) {
              bodyAimUpdate();
          }
          if (getCurrentWeaponMenuValue("Head Aim Override") == 1) {
              headAimUpdate();
          }
          if (getCurrentWeaponMenuValue("Minimum Damage Override") == 1) {
              minimumDamageUpdate();
          }
      }
  }
  
  function headAimUpdate() {
      for (i = 0; i < enemies.length; i++) {
          if (!Entity.IsAlive(enemies[i]) || Entity.IsDormant(enemies[i])) {
              continue;
          }
          flags = Entity.GetProp(enemies[i], "CCSPlayer", "m_fFlags");
          if (getCurrentWeaponMenuValue("Head Aim On") & (1 << 0)) {
              origin = Entity.GetRenderOrigin(enemies[i]);
              myself = Entity.GetRenderOrigin(localPlayer);
              distance_to_target = Math.sqrt(Math.pow(origin[0] - myself[0], 2) + Math.pow(origin[1] - myself[1], 2) + Math.pow(origin[2] - myself[2], 2)).toFixed(0);
              if (distance_to_target > getCurrentWeaponMenuValue("Head Aim Distance > X")) {
                  setHeadAim(enemies[i]);
                  continue;
              }
          }
          if (getCurrentWeaponMenuValue("Head Aim On") & (1 << 1)) {
              if (Entity.GetProp(enemies[i], "CBasePlayer", "m_flDuckAmount") > 0.1) {
                  setHeadAim(enemies[i]);
                  continue;
              }
          }
          if (getCurrentWeaponMenuValue("Head Aim On") & (1 << 2)) {
              if (!(flags & (1 << 0)) && !(flags & (1 << 12))) {
                  setHeadAim(enemies[i]);
                  continue;
              }
          }
          if (getCurrentWeaponMenuValue("Head Aim On") & (1 << 3)) {
              if (playerMissed[enemies[i]] > getCurrentWeaponMenuValue("Head Aim Misses > X")) {
                  setHeadAim(enemies[i]);
                  continue;
              }
          }
          if (getCurrentWeaponMenuValue("Head Aim On") & (1 << 4)) {
              if (getVelocity(enemies[i]) > 1 && getVelocity(enemies[i]) < 60 && !(flags & (1 << 1))) {
                  setHeadAim(enemies[i]);
                  continue;
              }
          }
          if (getCurrentWeaponMenuValue("Head Aim On") & (1 << 5)) {
              if (Entity.GetProp(enemies[i], "CBasePlayer", "m_iHealth") < getCurrentWeaponMenuValue("Head Aim HP < X")) {
                  setHeadAim(enemies[i]);
                  continue;
              }
          }
          if (getCurrentWeaponMenuValue("Head Aim On") & (1 << 6)) {
              origin = Entity.GetRenderOrigin(enemies[i]);
              myself = Entity.GetRenderOrigin(localPlayer);
              distance_to_target = Math.sqrt(Math.pow(origin[0] - myself[0], 2) + Math.pow(origin[1] - myself[1], 2) + Math.pow(origin[2] - myself[2], 2)).toFixed(0);
              if (distance_to_target < getCurrentWeaponMenuValue("Head Aim Distance < X")) {
                  setHeadAim(enemies[i]);
                  continue;
              }
          }
      }
  }
  
  function minimumDamageUpdate() {
      for (i = 0; i < enemies.length; i++) {
          if (!Entity.IsAlive(enemies[i]) || Entity.IsDormant(enemies[i])) {
              continue;
          }
          flags = Entity.GetProp(enemies[i], "CCSPlayer", "m_fFlags");
          if (getCurrentWeaponMenuValue("Minimum Damage On") & (1 << 0)) {
              origin = Entity.GetRenderOrigin(enemies[i]);
              myself = Entity.GetRenderOrigin(localPlayer);
              distance_to_target = Math.sqrt(Math.pow(origin[0] - myself[0], 2) + Math.pow(origin[1] - myself[1], 2) + Math.pow(origin[2] - myself[2], 2)).toFixed(0);
              if (distance_to_target > getCurrentWeaponMenuValue("Minimum Damage Distance > X")) {
                  setMinimumDamage(enemies[i]);
                  continue;
              }
          }
          if (getCurrentWeaponMenuValue("Minimum Damage On") & (1 << 1)) {
              if (Entity.GetProp(enemies[i], "CBasePlayer", "m_flDuckAmount") > 0.1) {
                  setMinimumDamage(enemies[i]);
                  continue;
              }
          }
          if (getCurrentWeaponMenuValue("Minimum Damage On") & (1 << 2)) {
              if (!(flags & (1 << 0)) && !(flags & (1 << 12))) {
                  setMinimumDamage(enemies[i]);
                  continue;
              }
          }
          if (getCurrentWeaponMenuValue("Minimum Damage On") & (1 << 3)) {
              if (playerMissed[enemies[i]] > getCurrentWeaponMenuValue("Minimum Damage Misses > X")) {
                  setMinimumDamage(enemies[i]);
                  continue;
              }
          }
          if (getCurrentWeaponMenuValue("Minimum Damage On") & (1 << 4)) {
              if (getVelocity(enemies[i]) > 1 && getVelocity(enemies[i]) < 60 && !(flags & (1 << 1))) {
                  setMinimumDamage(enemies[i]);
                  continue;
              }
          }
          if (getCurrentWeaponMenuValue("Minimum Damage On") & (1 << 5)) {
              if (Entity.GetProp(enemies[i], "CBasePlayer", "m_iHealth") < getCurrentWeaponMenuValue("Minimum Damage HP < X")) {
                  setMinimumDamage(enemies[i]);
                  continue;
              }
          }
          if (getCurrentWeaponMenuValue("Minimum Damage On") & (1 << 6)) {
              origin = Entity.GetRenderOrigin(enemies[i]);
              myself = Entity.GetRenderOrigin(localPlayer);
              distance_to_target = Math.sqrt(Math.pow(origin[0] - myself[0], 2) + Math.pow(origin[1] - myself[1], 2) + Math.pow(origin[2] - myself[2], 2)).toFixed(0);
              if (distance_to_target < getCurrentWeaponMenuValue("Minimum Damage Distance < X")) {
                  setMinimumDamage(enemies[i]);
                  continue;
              }
          }
      }
  }
  
  function safepointUpdate() {
      for (i = 0; i < enemies.length; i++) {
          if (!Entity.IsAlive(enemies[i]) || Entity.IsDormant(enemies[i])) {
              continue;
          }
          flags = Entity.GetProp(enemies[i], "CCSPlayer", "m_fFlags");
          if (getCurrentWeaponMenuValue("Safe Point On") & (1 << 0)) {
              origin = Entity.GetRenderOrigin(enemies[i]);
              myself = Entity.GetRenderOrigin(localPlayer);
              distance_to_target = Math.sqrt(Math.pow(origin[0] - myself[0], 2) + Math.pow(origin[1] - myself[1], 2) + Math.pow(origin[2] - myself[2], 2)).toFixed(0);
              if (distance_to_target > getCurrentWeaponMenuValue("Safe Point Distance > X")) {
                  setSafePoint(enemies[i]);
                  continue;
              }
          }
          if (getCurrentWeaponMenuValue("Safe Point On") & (1 << 1)) {
              if (Entity.GetProp(enemies[i], "CBasePlayer", "m_flDuckAmount") > 0.1) {
                  setSafePoint(enemies[i]);
                  continue;
              }
          }
          if (getCurrentWeaponMenuValue("Safe Point On") & (1 << 2)) {
              if (!(flags & (1 << 0)) && !(flags & (1 << 12))) {
                  setSafePoint(enemies[i]);
                  continue;
              }
          }
          if (getCurrentWeaponMenuValue("Safe Point On") & (1 << 3)) {
              if (playerMissed[enemies[i]] > getCurrentWeaponMenuValue("Safe Point Misses > X")) {
                  setSafePoint(enemies[i]);
                  continue;
              }
          }
          if (getCurrentWeaponMenuValue("Safe Point On") & (1 << 4)) {
              if (getVelocity(enemies[i]) > 1 && getVelocity(enemies[i]) < 60 && !(flags & (1 << 1))) {
                  setSafePoint(enemies[i]);
                  continue;
              }
          }
          if (getCurrentWeaponMenuValue("Safe Point On") & (1 << 5)) {
              if (Entity.GetProp(enemies[i], "CBasePlayer", "m_iHealth") < getCurrentWeaponMenuValue("Safe Point HP < X")) {
                  setSafePoint(enemies[i]);
                  continue;
              }
          }
          if (getCurrentWeaponMenuValue("Safe Point On") & (1 << 6)) {
              origin = Entity.GetRenderOrigin(enemies[i]);
              myself = Entity.GetRenderOrigin(localPlayer);
              distance_to_target = Math.sqrt(Math.pow(origin[0] - myself[0], 2) + Math.pow(origin[1] - myself[1], 2) + Math.pow(origin[2] - myself[2], 2)).toFixed(0);
              if (distance_to_target < getCurrentWeaponMenuValue("Safe Point Distance < X")) {
                  setSafePoint(enemies[i]);
                  continue;
              }
          }
      }
  }
  
  function bodyAimUpdate() {
      for (i = 0; i < enemies.length; i++) {
          if (!Entity.IsAlive(enemies[i]) || Entity.IsDormant(enemies[i])) {
              continue;
          }
          flags = Entity.GetProp(enemies[i], "CCSPlayer", "m_fFlags");
          if (getCurrentWeaponMenuValue("Body Aim On") & (1 << 0)) {
              origin = Entity.GetRenderOrigin(enemies[i]);
              myself = Entity.GetRenderOrigin(localPlayer);
              distance_to_target = Math.sqrt(Math.pow(origin[0] - myself[0], 2) + Math.pow(origin[1] - myself[1], 2) + Math.pow(origin[2] - myself[2], 2)).toFixed(0);
              if (distance_to_target > getCurrentWeaponMenuValue("Body Aim Distance > X")) {
                  setBodyAim(enemies[i]);
                  continue;
              }
          }
          if (getCurrentWeaponMenuValue("Body Aim On") & (1 << 1)) {
              if (Entity.GetProp(enemies[i], "CBasePlayer", "m_flDuckAmount") > 0.1) {
                  setBodyAim(enemies[i]);
                  continue;
              }
          }
          if (getCurrentWeaponMenuValue("Body Aim On") & (1 << 2)) {
              if (!(flags & (1 << 0)) && !(flags & (1 << 12))) {
                  setBodyAim(enemies[i]);
                  continue;
              }
          }
          if (getCurrentWeaponMenuValue("Body Aim On") & (1 << 3)) {
              if (playerMissed[enemies[i]] > getCurrentWeaponMenuValue("Body Aim Misses > X")) {
                  setBodyAim(enemies[i]);
                  continue;
              }
          }
          if (getCurrentWeaponMenuValue("Body Aim On") & (1 << 4)) {
              if (getVelocity(enemies[i]) > 1 && getVelocity(enemies[i]) < 60 && !(flags & (1 << 1))) {
                  setBodyAim(enemies[i]);
                  continue;
              }
          }
          if (getCurrentWeaponMenuValue("Body Aim On") & (1 << 5)) {
              if (Entity.GetProp(enemies[i], "CBasePlayer", "m_iHealth") < getCurrentWeaponMenuValue("Body Aim HP < X")) {
                  setBodyAim(enemies[i]);
                  continue;
              }
          }
          if (getCurrentWeaponMenuValue("Body Aim On") & (1 << 6)) {
              origin = Entity.GetRenderOrigin(enemies[i]);
              myself = Entity.GetRenderOrigin(localPlayer);
              distance_to_target = Math.sqrt(Math.pow(origin[0] - myself[0], 2) + Math.pow(origin[1] - myself[1], 2) + Math.pow(origin[2] - myself[2], 2)).toFixed(0);
              if (distance_to_target < getCurrentWeaponMenuValue("Body Aim Distance < X")) {
                  setBodyAim(enemies[i]);
                  continue;
              }
          }
      }
  }
  
  function onMenuUpdate() {
      if (!UI.IsMenuOpen()) {
          return;
      }
      hideAllItems();
      showActiveItems();
  }
  
  //----------------------------------------------------------------------------\\
  
  function setHideShots(shouldHideShots) {
      if (shouldHideShots) {
          if (!UI.GetValue(["Rage", "Exploits", "Keys", "Key assignment", "Hide shots"])) {
              UI.ToggleHotkey(["Rage", "Exploits", "Keys", "Key assignment", "Hide shots"]);
          }
      } else {
          if (UI.GetValue(["Rage", "Exploits", "Keys", "Key assignment", "Hide shots"])) {
              UI.ToggleHotkey(["Rage", "Exploits", "Keys", "Key assignment", "Hide shots"]);
          }
      }
  }
  
  function setDamageMode(mode) {
      damageMode = mode;
      if (damageMode == "Idle") {
          originalDamage = 0;
      } else {
          originalDamage = UI.GetValue(["Rage", "Target", currentWeapon, mode + " Damage"]);
          if (originalDamage == 0) {
              originalDamage = UI.GetValue(["Rage", "Target", "General", mode + " Damage"]);
          }
      }
      UI.SetValue(["Rage", "Target", "General", "Minimum damage"], originalDamage);
      UI.SetValue(["Rage", "Target", currentWeapon, "Minimum damage"], originalDamage);
  }
  
  function setHitboxes(mode) {
      hitboxMode = mode;
      if (mode == "Idle") {
          originalHitboxes = 255;
          originalHitboxes1 = 255;
      } else if (mode == "Head") {
          originalHitboxes = 1;
          originalHitboxes1 = 1;
      } else {
          originalHitboxes = UI.GetValue(["Rage", "Target", currentWeapon, mode + " Hitboxes"]);
          if (originalHitboxes == 0) {
              originalHitboxes = UI.GetValue(["Rage", "Target", "General", mode + " Hitboxes"]);
          }
          originalHitboxes1 = UI.GetValue(["Rage", "Target", currentWeapon, mode + " Multipoint Hitboxes"]);
          if (originalHitboxes1 == 0) {
              originalHitboxes1 = UI.GetValue(["Rage", "Target", "General", mode + " Multipoint Hitboxes"]);
          }
      }
      UI.SetValue(["Rage", "Target", "General", "Hitboxes"], originalHitboxes);
      UI.SetValue(["Rage", "Target", "General", "Multipoint hitboxes"], originalHitboxes1);
      UI.SetValue(["Rage", "Target", currentWeapon, "Hitboxes"], originalHitboxes);
      UI.SetValue(["Rage", "Target", currentWeapon, "Multipoint hitboxes"], originalHitboxes1);
  }
  
  function setAccuracyMode(mode) {
      accuracyMode = mode;
      if (mode == "Idle") {
          originalAccuracy = 100;
      } else {
          originalAccuracy = UI.GetValue(["Rage", "Target", currentWeapon, mode + " Hitchance"]);
          if (originalAccuracy == 0) {
              originalAccuracy = UI.GetValue(["Rage", "Target", "General", mode + " Hitchance"]);
          }
      }
      UI.SetValue(["Rage", "Accuracy", "General", "Hitchance"], originalAccuracy);
      UI.SetValue(["Rage", "Accuracy", currentWeapon, "Hitchance"], originalAccuracy);
  }
  
  function setSafePoint(player) {
      Ragebot.ForceTargetSafety(player);
      Entity.DrawFlag(player, "SAFEPOINT", [0, 255, 255, 255])
  }
  
  function setHeadAim(player) {
      if (rageTarget == player) {
          UI.SetValue(["Rage", "Target", currentWeapon, "Hitboxes"], 1);
          UI.SetValue(["Rage", "Target", "General", "Hitboxes"], 1);
          UI.SetValue(["Rage", "Target", currentWeapon, "Multipoint hitboxes"], 1);
          UI.SetValue(["Rage", "Target", "General", "Multipoint hitboxes"], 1);
      }
      Entity.DrawFlag(player, "HEAD", [255, 0, 0, 255])
  }
  
  function setBodyAim(player) {
      if (rageTarget == player) {
          if (UI.GetValue(["Rage", "Target", currentWeapon, "Hitboxes"]) > 0 && UI.GetValue(["Rage", "Target", currentWeapon, "Hitboxes"]) % 2 == 1) {
              UI.SetValue(["Rage", "Target", currentWeapon, "Hitboxes"], UI.GetValue(["Rage", "Target", currentWeapon, "Hitboxes"]) - 1);
              UI.SetValue(["Rage", "Target", "General", "Hitboxes"], UI.GetValue(["Rage", "Target", currentWeapon, "Hitboxes"]) - 1);
          }
          if (UI.GetValue(["Rage", "Target", currentWeapon, "Multipoint hitboxes"]) > 0 && UI.GetValue(["Rage", "Target", currentWeapon, "Multipoint hitboxes"]) % 2 == 1) {
              UI.SetValue(["Rage", "Target", currentWeapon, "Multipoint hitboxes"], UI.GetValue(["Rage", "Target", currentWeapon, "Multipoint hitboxes"]) - 1);
              UI.SetValue(["Rage", "Target", "General", "Multipoint hitboxes"], UI.GetValue(["Rage", "Target", currentWeapon, "Multipoint hitboxes"]) - 1);
          }
      }
      Entity.DrawFlag(player, "BAIM", [255, 0, 255, 255])
  }
  
  function setMinimumDamage(player) {
      if (rageTarget == player && damageMode!="Minimum") {
          UI.SetValue(["Rage", "Target", currentWeapon, "Minimum damage"], UI.GetValue(["Rage", "Accuracy", currentWeapon, "Override Minimum Damage"]));
          UI.SetValue(["Rage", "Target", "General", "Minimum damage"], UI.GetValue(["Rage", "Accuracy", currentWeapon, "Override Minimum Damage"]));
          damageMode = "Override";
      }
      Entity.DrawFlag(player, "MINDMG", [0, 255, 0, 255])
  }
  ```

## 总结

小于10%的原创代码，不愧是*代码的搬运工*，直接给整个OP论坛和泄露JS都paste来辣

这种左沾右沾的狗屎听说还能卖钱是我**万万没想到**的

希望大家能擦亮双眼，拒绝面向复制粘贴土狗
