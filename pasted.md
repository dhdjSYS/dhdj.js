# 某pasted js的详细分析 附源码

今天收到了一位网友发来的js，说是c+v的，让我看看并公开了

打开一看 啊，果不其然 一眼扫去基本上80%都是paste，paste以外的部分写的像狗屎 性能优化极差 加载一下op都卡了。

那么下面是源码

## 源码

```javascript
/********************************************
*
*              XXXXXX XXXXX
*            Create XXXXXXX
*               QQ：XXXXXXX
*        使用前请更改uid检查变量 就在下面
*           
********************************************/

//--> welcome
const initialize = function () {
    Cheat.PrintChat(" \x04>>Welcome to \x01Control\x06sense\x04<<\x01 ");
    Cheat.PrintChat(" \x04>>祝您游戏愉快<<\x01 ");
    Cheat.PrintChat(" \x04>>Q1104391380<<\x01 ");
}

//--> UID 检查

//menu misc UI-----------------------------------------------------------------
UI.AddSubTab(["Config", "SUBTAB_MGR"], "PASTED menu misc.");
UI.AddSliderInt(["Config", "PASTED menu misc.", "PASTED menu misc."], "--> Menu Indicator && Visual <--", 0, 0);
UI.AddCheckbox(["Config", "PASTED menu misc.", "PASTED menu misc."], "Menu indicator");
UI.AddCheckbox(["Config", "PASTED menu misc.", "PASTED menu misc."], "Bar text indicator");
UI.AddCheckbox(["Config", "PASTED menu misc.", "PASTED menu misc."], "Health bar indicator");
UI.AddCheckbox(["Config", "PASTED menu misc.", "PASTED menu misc."], "Top RGB line");
UI.AddCheckbox(["Config", "PASTED menu misc.", "PASTED menu misc."], "Enable C4 Indicator");
UI.AddCheckbox(["Config", "PASTED menu misc.", "PASTED menu misc."], "Crosshair hitmarker");
UI.AddCheckbox(["Config", "PASTED menu misc.", "PASTED menu misc."], "Crosshair Dmg log");
UI.AddCheckbox(["Config", "PASTED menu misc.", "PASTED menu misc."], "AA indicator");
UI.AddDropdown(["Config", "PASTED menu misc.", "PASTED menu misc."], "AA indicator mode", ["Ideal yaw", "Half triangle"], 0)
UI.AddCheckbox(["Config", "PASTED menu misc.", "PASTED menu misc."], "Show Bullet Tracer");
UI.AddSliderInt(["Config", "PASTED menu misc.", "PASTED menu misc."], "Bullet Tracer Thickness", 2, 50);
UI.AddColorPicker(["Config", "PASTED menu misc.", "PASTED menu misc."], "Bullet Tracer Color");
UI.AddCheckbox(["Config", "PASTED menu misc.", "PASTED menu misc."], "RGB Tracer Color");
UI.AddCheckbox(["Config", "PASTED menu misc.", "PASTED menu misc."], "Enable smoke radius");
UI.AddColorPicker(["Config", "PASTED menu misc.", "PASTED menu misc."], "Smoke line color");
UI.AddColorPicker(["Config", "PASTED menu misc.", "PASTED menu misc."], "Smoke radius color");
UI.AddCheckbox(["Config", "PASTED menu misc.", "PASTED menu misc."], "Enable free camera");
UI.AddSliderInt(["Config", "PASTED menu misc.", "PASTED menu misc."], "Max free camera follow value", 5, 30);
UI.AddSliderFloat(["Config", "PASTED menu misc.", "PASTED menu misc."], "Hit effect", 0, 2);
UI.AddCheckbox(["Config", "PASTED menu misc.", "PASTED menu misc."], "Enable menu watermark");
UI.AddColorPicker(["Config", "PASTED menu misc.", "PASTED menu misc."], "Watermark color");
UI.AddSliderInt(["Config", "PASTED menu misc.", "PASTED menu misc."], "--> Menu advanced log <--", 0, 0);
UI.AddCheckbox(["Config", "PASTED menu misc.", "PASTED menu misc."], "Log in chat");
UI.AddCheckbox(["Config", "PASTED menu misc.", "PASTED menu misc."], "Buy Logs");
UI.AddCheckbox(["Config", "PASTED menu misc.", "PASTED menu misc."], "Dmg Logs");
UI.AddCheckbox(["Config", "PASTED menu misc.", "PASTED menu misc."], "Vote Logs");
UI.AddSliderInt(["Config", "PASTED menu misc.", "PASTED menu misc."], "--> Menu RageBot assist <--", 0, 0);
UI.AddCheckbox(["Config", "PASTED menu misc.", "PASTED menu misc."], "AWP&Scout Flip");
UI.AddCheckbox(["Config", "PASTED menu misc.", "PASTED menu misc."], "SemiRage assist");
UI.AddCheckbox(["Config", "PASTED menu misc.", "PASTED menu misc."], "Trigger rage autowall");
UI.AddCheckbox(["Config", "PASTED menu misc.", "PASTED menu misc."], "Double Tap assist");
UI.AddCheckbox(["Config", "PASTED menu misc.", "PASTED menu misc."], "DT DMG perdiction");
UI.AddCheckbox(["Config", "PASTED menu misc.", "PASTED menu misc."], "Better DT recharge");
UI.AddCheckbox(["Config", "PASTED menu misc.", "PASTED menu misc."], "Jump Scout/Revolver Hitchance");
UI.AddSliderInt(["Config", "PASTED menu misc.", "PASTED menu misc."], "Hitchance", 0, 100);
UI.AddSliderInt(["Config", "PASTED menu misc.", "PASTED menu misc."], "-- Slowwalk speed --", 0, 0);
UI.AddSliderInt(["Config", "PASTED menu misc.", "PASTED menu misc."], "Speed", 0, 135);
UI.AddCheckbox(["Config", "PASTED menu misc.", "PASTED menu misc."], "Jitter Speed");
UI.AddSliderInt(["Config", "PASTED menu misc.", "PASTED menu misc."], "Jitter Min", 0, 135);
UI.AddSliderInt(["Config", "PASTED menu misc.", "PASTED menu misc."], "Jitter Max", 0, 135);
UI.AddCheckbox(["Config", "PASTED menu misc.", "PASTED menu misc."], "Individual speeds");
UI.AddSliderInt(["Config", "PASTED menu misc.", "PASTED menu misc."], "Forward Speed", 0, 135);
UI.AddSliderInt(["Config", "PASTED menu misc.", "PASTED menu misc."], "Side Speed", 0, 135);
UI.AddSliderInt(["Config", "PASTED menu misc.", "PASTED menu misc."], "Back Speed", 0, 135);
UI.AddSliderInt(["Config", "PASTED menu misc.", "PASTED menu misc."], "-- Pitch misc. --", 0, 0);
UI.AddDropdown(["Config", "PASTED menu misc.", "PASTED menu misc."], "Pitch set", ["Off", "Pitch zero", "Pitch zero on land", "Pitch down", "Fake pitch down"], 0);
UI.AddSliderInt(["Config", "PASTED menu misc.", "PASTED menu misc."], "--> Menu Other misc. <--", 0, 0);
UI.AddCheckbox(["Config", "PASTED menu misc.", "PASTED menu misc."], "Enable Rainow HUD");
UI.AddSliderFloat(["Config", "PASTED menu misc.", "PASTED menu misc."], "Colour Switch Speed", 0.02, 1);
UI.AddCheckbox(["Config", "PASTED menu misc.", "PASTED menu misc."], "Enable Aspect Ratio Changer");
UI.AddSliderFloat(["Config", "PASTED menu misc.", "PASTED menu misc."], "Aspect Ratio", 0.5, 3.10);
UI.AddCheckbox(["Config", "PASTED menu misc.", "PASTED menu misc."], "Enable Clantag Changer");
UI.AddDropdown(["Config", "PASTED menu misc.", "PASTED menu misc."], "Clantag", ["None", "Onetap.com", "CFG By Ye pack", "Custom"], 0)
UI.AddTextbox(["Config", "PASTED menu misc.", "PASTED menu misc."], "Custom Clantag")
UI.AddDropdown(["Config", "PASTED menu misc.", "PASTED menu misc."], "Clantag Animation", ["Static", "Flash", "Scroll Left", "Scroll Right", "Type Left", "Type Right"], 0)
UI.AddSliderInt(["Config", "PASTED menu misc.", "PASTED menu misc."], "Clantag Speed", 1, 50);
if (UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Aspect Ratio"]) == 0) {
    UI.SetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Aspect Ratio"], 1.50);
}
if (UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Speed"]) == 0) {
    UI.SetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Speed"], 40);
}
UI.AddHotkey(["Config", "SUBTAB_MGR", "Scripts", "SHEET_MGR", "Keys", "JS Keybinds"], "Autowall", "Trigger Autowall");
//menu misc UI-----------------------------------------------------------------

//Weapon Config Menu
//----------------------------------------------------------------------------\\
//主菜单
UI.AddSubTab(["Config", "SUBTAB_MGR"], "Weapon Config");
UI.AddCheckbox(["Config", "Weapon Config", "Weapon Config"], "Enable Weapon Config");
UI.AddSliderInt(["Config", "Weapon Config", "Weapon Config"], ">>-PASTED Weapon Config -<<", 0, 0);
UI.AddCheckbox(["Config", "Weapon Config", "Weapon Config"], "Automatic Mindmg");
UI.AddSliderInt(["Config", "Weapon Config", "Weapon Config"], "Automatic Mindmg Offset", 1, 20);
UI.AddSliderInt(["Config", "Weapon Config", "Weapon Config"], "", -1, 0);
UI.AddCheckbox(["Config", "Weapon Config", "Weapon Config"], "Enable Rage Optimization");
UI.AddSliderInt(["Config", "Weapon Config", "Weapon Config"], ">>-PASTED Rage Optimization -<<", 0, 0);
UI.AddCheckbox(["Config", "Weapon Config", "Weapon Config"], "Teleport");
//按键
UI.AddHotkey( ["Rage", "General", "General", "Key assignment"], "Minimum damage", "Mindmg");
UI.AddHotkey( ["Rage", "General", "General", "Key assignment"], "Minimum accuracy", "Minac");
//----------------------------------------------------------------------------\\

//Menu indicator-----------------------------------------------------------------

//--> RGB line

function line() {
    var screen_width = Math.round(Global.GetScreenSize()[0]);
    var me = Entity.GetLocalPlayer();
    if (UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Menu indicator"]) && UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Top RGB line"]) && Entity.IsAlive(me)) {
        var colors = HSVtoRGB(Globals.Realtime() / 5 % 1, 1, 1)
        Render.GradientRect(0, 0, screen_width / 2, 4, 1, [colors.g, colors.b, colors.r, 255], [colors.r, colors.g, colors.b, 255]);
        Render.GradientRect(screen_width / 2, 0, screen_width / 2, 4, 1, [colors.r, colors.g, colors.b, 255], [colors.b, colors.r, colors.g, 255]);
    }
}

//--> RGB line


//--> AA indicator 

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

function Draw_invert() {
    var local = Entity.GetLocalPlayer();
    line();
    DrawThread();
    dispDamage()
    if (UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Crosshair Dmg log"])) {
        render_damage_logs();
    }
    if (UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Menu indicator"]) && UI.IsMenuOpen()) {
        drawMenuBorder();
    }
    if (Entity.IsAlive(local) && UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "AA indicator"]) && UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "AA indicator mode"]) == 0) {
        Renderer.Desync();
    }
    if (Entity.IsAlive(local) && UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "AA indicator"]) && UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "AA indicator mode"]) == 1) {
        AA_indicator();
    }
};

//--> AA indicator 

//--> Menu bar indicator

const modules = [
{
     label: "FAKE",
     color_1: {
        dormant: [186, 0, 16, 225],
        active: [154, 205, 50, 255]
    },
    logic: function () {
        const real = Local.GetRealYaw(),
            fake = Local.GetFakeYaw();
        const delta = Math.abs(normalize_yaw(real % 360 - fake % 360)) / 2;
        return delta / 60;
    }
}
];

var notspam = 0;
var netspam = 0;
var whit = 0;
var health2 = 0;
var armor2 = 0;
var tab = "General"
var weapon = 507
var health_hurt = false
const DrawThread = function() {
    var indicator = UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Menu indicator"])
    var customFont = Render.AddFont("segoeuib.ttf", 24, 400);
    var customFont_big = Render.AddFont("segoeuib.ttf", 25, 800);
    var screen_size = Global.GetScreenSize();
    var fl_limit =UI.GetValue(["Rage", "Fake Lag", "General", "Limit"]);
    var fl_jitter =UI.GetValue(["Rage", "Fake Lag", "General", "Jitter"]);
    var fl_tlimit =UI.GetValue(["Rage", "Fake Lag", "General", "Trigger limit"]);
    var ChokeFL = Globals.ChokedCommands();
    var real_1 = Local.GetRealYaw(),
        fake_1 = Local.GetFakeYaw();
    var DMG = UI.GetValue(["Rage", "Target", tab,"Minimum damage"])
    var HC_flag = UI.GetValue(["Rage", "Accuracy", tab,"Hitchance"])
const delta = Math.abs(normalize_yaw(real_1 % 360 - fake_1 % 360)) / 2;
    if (DMG == 0) {
    var DMG = "AUTO"
    }
    if (weapon == 507) {
     var DMG = "AUTO"
     var HC_flag = "100"
    }
    var tickcount_1 = Global.Tickcount();
    var color = RGB(tickcount_1 % 350 / 350, 1, 1, 1, 255);
    UI.SetColor(["Config", "Cheat", "General", "Log color"], [color.r, color.g, color.b, 220]);
   for (var i = 0; i < modules.length; i++) {
         mod = modules[i];
         result_1 = mod.logic();
        color_fake = [
            mod.color_1.dormant[0] + (mod.color_1.active[0] - mod.color_1.dormant[0]) * result_1,
            mod.color_1.dormant[1] + (mod.color_1.active[1] - mod.color_1.dormant[1]) * result_1,
            mod.color_1.dormant[2] + (mod.color_1.active[2] - mod.color_1.dormant[2]) * result_1,
            255
        ];
    }
    if (indicator && UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Bar text indicator"]) && Entity.IsAlive(Entity.GetLocalPlayer())) {
        Render.GradientRect(2, screen_size[1] / 1.78, 150, 26, 1, [0, 0, 0, 100], [0, 0, 0, 0]);
        Render.String(3, screen_size[1] / 1.8, 0, "CFG By Ye", [94, 231, 237, 150], customFont_big);
        Render.String(8, screen_size[1] / 1.8, 0, "CFG By Ye", [223, 91, 164, 200], customFont);
/*         Render.String(6, screen_size[1] / 1.8, 0, "Control", [color.r, color.g, color.b, 200], customFont);
        Render.String(94, screen_size[1] / 1.8, 0, "sense", [3, 131, 31, 200], customFont); */
        Render.GradientRect(2, screen_size[1] / 1.69, 70, 25, 1, [0, 0, 0, 100], [0, 0, 0, 0]);
        Render.String(1, screen_size[1] / 1.7, 0, "FL", [0, 0, 0, 150], customFont_big);
        Render.String(3, screen_size[1] / 1.7, 0, "FL", [192, color.g, 32, 240], customFont);
        Render.String(38, screen_size[1] / 1.7, 0, ""+fl_limit+" - "+fl_jitter+" - "+fl_tlimit, [192, color.g, 32, 240], customFont);
       /*  draw_arc(38, screen_size[1] / 1.655, 9.3, 1, 500, 5, [25, 25, 25, 190]);
        draw_arc(38, screen_size[1] / 1.655, 8, 1, ChokeFL * 40, 5, [192, color.g, 32, 240]); */
        Render.GradientRect(2, screen_size[1] / 1.6, 100, 26, 1, [0, 0, 0, 100], [0, 0, 0, 0]);
        Render.String(1, screen_size[1] / 1.61, 0, mod.label, [0, 0, 0, 150], customFont_big);
        draw_arc(72, screen_size[1] / 1.57, 9.3, 1, 500, 5, [25, 25, 25, 190]);
        Render.String(3, screen_size[1] / 1.61, 0, mod.label, color_fake, customFont);
        draw_arc(72, screen_size[1] / 1.57, 8, 1, delta * 6, 5, color_fake);
        Render.GradientRect(2, screen_size[1] / 1.52, 180, 26, 1, [0, 0, 0, 100], [0, 0, 0, 0]);
        Render.String(1, screen_size[1] / 1.53, 0, "DMG => " + DMG, [0, 0, 0, 150], customFont_big);
        Render.String(3, screen_size[1] / 1.53, 0, "DMG => " + DMG, [160, 160, 255, 255], customFont);
        Render.GradientRect(2, screen_size[1] / 1.45, 180, 26, 1, [0, 0, 0, 100], [0, 0, 0, 0]);
        Render.String(1, screen_size[1] / 1.46, 0, "HC => "+HC_flag+"%", [0, 0, 0, 150], customFont_big);
        Render.String(3, screen_size[1] / 1.46, 0, "HC => "+HC_flag+"%", [160, 160, 255, 255], customFont);
        Render.GradientRect(2, screen_size[1] / 1.385, 180, 26, 1, [0, 0, 0, 100], [0, 0, 0, 0]);
        if (UI.GetValue(["Rage", "Anti Aim", "General", "Key assignment", "AA Direction inverter"]) == 1) {
            Render.String(1, screen_size[1] / 1.395, 0, "AA => Left", [0, 0, 0, 150], customFont_big);
            Render.String(3, screen_size[1] / 1.395, 0, "AA => Left", [160, 160, 255, 255], customFont);
        } else {
            Render.String(1, screen_size[1] / 1.395, 0, "AA => Right", [0, 0, 0, 150], customFont_big);
            Render.String(3, screen_size[1] / 1.395, 0, "AA => Right", [160, 160, 255, 255], customFont);
        }
    }
    if (indicator && UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Health bar indicator"]) && Entity.IsAlive(Entity.GetLocalPlayer())) {
        if (!Entity.IsValid(Entity.GetLocalPlayer())) return
        var health = Entity.GetProp(Entity.GetLocalPlayer(), "CBasePlayer", "m_iHealth");
        var armor = Entity.GetProp(Entity.GetLocalPlayer(), "CCSPlayerResource", "m_iArmor");
        if (health2 != health) {
            if (health2 < health) {
                health2 = health2 + 1;
            } else {
                health2 = health2 - 1;
            }
        }
        if (armor2 != armor) {
            if (armor2 < armor) {
                 armor2 = armor2 + 1;
            } else {
                 armor2 = armor2 - 1;
            }
        }
        var text = "" + health2;
        var text2 = "" + armor2;
        if (health_hurt) {
            var red = 255
            var green = 0
        }else{
            var red = 255 - (health2 * 2.55);
            var green = health2 * 2.55
        }
        var font = Render.AddFont("Arial", 20, 100);
        if (Entity.IsAlive(Entity.GetLocalPlayer())) {
            //hp
            Render.Rect(25, Render.GetScreenSize()[1] - 27, 116, 14, [whit, whit, whit, 200]);
            Render.String(99, Render.GetScreenSize()[1] - 56, 0, "HP", [0, 0, 0, 255], font);
            Render.String(100, Render.GetScreenSize()[1] - 55, 0, "HP", [255, 255, 255, 255], font);
            Render.String(27, Render.GetScreenSize()[1] - 56, 0, text, [0, 0, 0, 255], font);
            Render.String(28, Render.GetScreenSize()[1] - 55, 0, text, [red, green, 0, 255], font);
            Render.FilledRect(26, Render.GetScreenSize()[1] - 25, (health2 * 1.145), 12, [red, green, 0, 255]);
            //armor
            Render.Rect(174, Render.GetScreenSize()[1] - 27, 160, 14, [whit, whit, whit, 200]);
            Render.String(244, Render.GetScreenSize()[1] - 56, 0, "ARMOR", [0, 0, 0, 255], font);
            Render.String(245, Render.GetScreenSize()[1] - 55, 0, "ARMOR", [255, 255, 255, 255], font);

            Render.String(173, Render.GetScreenSize()[1] - 56, 0, text2, [0, 0, 0, 255], font);
            Render.String(174, Render.GetScreenSize()[1] - 55, 0, text2, [7, 169, 232, 255], font);
            Render.FilledRect(175, Render.GetScreenSize()[1] - 25, (armor2 * 1.58), 12, [7, 169, 232, 255]);
            if ((UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Menu indicator"])) && (notspam == 0)) {
                Cheat.ExecuteCommand("hidehud 8");
                 notspam = 1;
            }
            if (netspam == 1) {
                Cheat.ExecuteCommand("hidehud 8");
                netspam = 0;
            }
        } else {
            if (netspam == 0) {
                Cheat.ExecuteCommand("hidehud 0");
                netspam = 1;
            }
        }
    } else {
        if (notspam == 1) {
            Cheat.ExecuteCommand("hidehud 0");
             notspam = 0;
        }
    }
}

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
            [screen_size[0] / 2 - 75, screen_size[1] / 2 + 16]
        ], realBorderColor);
    }
}

var Menu_alpha = 1
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


//--> Menu bar indicator

//Menu indicator-----------------------------------------------------------------


//--> hitmarker

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
var script = {
    shared: {
        choke_history: [0, 0, 0, 0],
        choke_max: 0,
        choke_inactive: false,
        desync: 0,
        speed: 0
    },
    position: {
        doubletap: {
            x: 10,
            y: 10
        },
        fakelag: {
            x: 10,
            y: 10
        },
        misc: {
            x: 10,
            y: 10
        }
    },
    hurt_logs: []
};

const render_damage_logs = function () {
    const font = Render.AddFont("Verdana", 10, 800);
    const x = Render.GetScreenSize()[0] / 2,
        y = Render.GetScreenSize()[1] / 2;
    for (var i = 0; i < script.hurt_logs.length; i++) {
        const current = script.hurt_logs[i];
        script.hurt_logs[i].anim_time = Math.min(script.hurt_logs[i].anim_time + Globals.Frametime() / 5, 1);
        if (current.anim_time === 1) {
            script.hurt_logs.slice(i, 1);
            continue;
        }
        Render.String(x - 20, y - 15 - i * 14, 1, "-" + current.dmg, [146, 255, 92, 200 * (1 - current.anim_time)], font);
        Render.String(x + 5, y - 15 - i * 14, 0, current.name, [235, 235, 235, 200 * (1 - current.anim_time)], font);
        if (current.dead) {
            const width = Render.TextSize(current.name, 3);
            Render.Line(x + 2, y - 10 - i * 14, x + width[0] + 8, y - 10 - i * 14, [235, 45, 45, 200 * (1 - current.anim_time)]);
        }
    }
}
const player_damage_handler = function () {
    const me = Entity.GetLocalPlayer();
    const userid = Entity.GetEntityFromUserID(Event.GetInt("userid"))
    const attacker = Entity.GetEntityFromUserID(Event.GetInt("attacker"));
    if (me == attacker && me != userid) {
        const dmg = Event.GetInt("dmg_health");
        const hp = Event.GetInt("health");
        script.hurt_logs.unshift({
            name: Entity.GetName(userid),
            dmg: dmg,
            dead: hp <= 0,
            anim_time: 0
        });
        if (script.hurt_logs.length > 10)
            script.hurt_logs.pop();
    }
}

//--> hitmarker


//log in chat---------------------------------------------------------------------


//--> Vote logs

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

//--> Vote logs


//--> Buy logs

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

//--> Buy logs


//--> DMG logs

log_hitboxes = [
    '默认',
    '头部',
    '胸部',
    '胃部',
    '左手',
    '右手',
    '左脚',
    '右脚',
    '???'
];

function getHitboxName(index) {
    switch (index) {
        case 0:
            hitboxName = "everything";
            break;
        case 1:
            hitboxName = "head";
            break;
        case 2:
            hitboxName = "chest";
            break;
        case 3:
            hitboxName = "stomach";
            break;
        case 4:
            hitboxName = "left hand";
            break;
        case 5:
            hitboxName = "right hand";
            break;
        case 6:
            hitboxName = "left leg";
            break;
        case 7:
            hitboxName = "right leg";
            break;

    }
    return hitboxName;
}

function HitgroupName(index) {
    return log_hitboxes[index] || 'body';
}

function ragebot_fire_1() {
    HC = Ragebot.GetTargetHitchance() + "%"
}

function weaponlist(a) {
    var letter = ""
    switch (a) {
        case "desert eagle":
            letter = "沙漠之鹰"
            break
        case "dual berettas":
            letter = "双枪"
            break
        case "five seven":
            letter = "FN57"
            break
        case "glock 18":
            letter = "格洛克 18 型"
            break
        case "ak 47":
            letter = "AK-47"
            break
        case "aug":
            letter = "AUG"
            break
        case "awp":
            letter = "大狙"
            break
        case "famas":
            letter = "法玛斯"
            break
        case "m249":
            letter = "M249"
            break
        case "g3sg1":
            letter = "匪家连狙"
            break
        case "galil ar":
            letter = "加利尔 AR"
            break
        case "m4a4":
            letter = "M4A4"
            break
        case "m4a1 s":
            letter = "M4A1 消音型"
            break
        case "mac 10":
            letter = "匪家吹风机"
            break
        case "p2000":
            letter = "P2000"
            break
        case "mp5 sd":
            letter = "MP5-SD"
            break
        case "ump 45":
            letter = "UMP-45"
            break

        case "xm1014":
            letter = "XM1014"
            break
        case "pp bizon":
            letter = "PP-野牛"
            break
        case "mag 7":
            letter = "MGA-7"
            break
        case "negev":
            letter = "内格夫"
            break
        case "sawed off":
            letter = "截短霰弹枪"
            break
        case "tec 9":
            letter = "TEC-9"
            break
        case "zeus x27":
            letter = "电击枪"
            break
        case "p250":
            letter = "P250"
            break
        case "mp7":
            letter = "MP7"
            break
        case "mp9":
            letter = "警家吹风机"
            break
        case "nova":
            letter = "新星"
            break
        case "p90":
            letter = "P90"
            break
        case "scar 20":
            letter = "警家连狙"
            break
        case "sg 553":
            letter = "SG-553"
            break
        case "ssg 08":
            letter = "鸟狙"
            break
        case "knife":case "bayonet":case "flip knife":case "gut knife":case "karambit":case "m9 bayonet":case "huntsman knife":case "bowie knife":case "butterfly knife":case "shadow daggers":case "falchion knife":case "ursus knife":case "navaja knife":case "stiletto knife":case "skeleton knife":case "nomad knife":case "survival knife":case "paracord knife":case "classic knife":case "talon knife":
            letter = "刀"
            break
        case "flashbang":
            letter = "闪光弹"
            break
        case "high explosive grenade":
            letter = "高爆手雷"
            break
        case "smoke grenade":
            letter = "烟雾弹"
            break
        case "molotov":
            letter = "燃烧弹"
            break
        case "decoy grenade":
            letter = "诱饵手雷"
            break
        case "incendiary grenade":
            letter = "燃烧弹"
            break
        case "c4 explosive":
            letter = "C4炸弹"
            break
        case "usp s":
            letter = "USP 消音版"
            break
        case "cz75 auto":
            letter = "CZ75 自动手枪"
            break
        case "r8 revolver":
            letter = "R8 左轮手枪"
            break
        default:
            letter = "未知武器"
            break
    }
    return letter
}

function hurt() {
    if (UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Dmg Logs"]) && UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Log in chat"])) {
        var localplayer_index = Entity.GetLocalPlayer();
        var localplayer_weapon = Entity.GetWeapon(localplayer_index);
        var weapon_name = Entity.GetName(localplayer_weapon);
        var attacker = Event.GetInt("attacker");
        var player = Entity.GetEntityFromUserID(Event.GetInt("userid"));
        var health = Event.GetInt("dmg_health");
        var hitbox = Event.GetString("hitgroup");
        var hp = 100 - Event.GetInt("health")
        var remainhp = Event.GetInt("health")
        if (hp >= 100) {
            var hp = "已死亡"
        }
if (Entity.GetEntityFromUserID(Event.GetInt("userid")) == Entity.GetLocalPlayer()) {
health_hurt = true
}else{
health_hurt = false
}

        tickcount = Global.Tickcount();
        color = RGB(tickcount % 350 / 350, 1, 1, 1, 255);
        if (Entity.IsLocalPlayer(Entity.GetEntityFromUserID(attacker))) {
            Cheat.PrintChat("\x01[ Control\x06sense\x01 ] 伤害 \x07" + Entity.GetName(player) + " \x01 使用\x07 " + weaponlist(weapon_name) + " \x01 给予伤害\x07 " + health + " \x01 命中点\x07 " + HitgroupName(hitbox) + " \x01[\x06命中率:" + HC + "\x01, \x06血量: \x07" + hp + "\x01/\x08" + remainhp + "\x01].\n");
            Cheat.PrintColor([color.r, color.g, color.b, 255], "\x01[ Control\x04sense\x01 ] 伤害 \x07" + Entity.GetName(player) + " \x01 使用\x07 " + weaponlist(weapon_name) + " \x01 给予伤害\x07 " + health + " \x01 命中点\x07 " + HitgroupName(hitbox) + " \x01[\x04命中率:" + HC + "\x01,\x04血量:" + hp + "/" + remainhp  + "\x01].\n")
        }
    }
}

//--> DMG logs


//log in chat---------------------------------------------------------------------


//--> C4 indicator

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

//--> C4 indicator


//--> Filp swich weapon

var flip = false

function on_weapon_fire() {
    me = Entity.GetLocalPlayer();
    short = Event.GetInt("userid")
    short_index = Entity.GetEntityFromUserID(short);
    localplayer_weapon = Entity.GetWeapon(me);
    var weapon_name_1 = Entity.GetName(localplayer_weapon);
    if (UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "AWP&Scout Flip"]) == true) {
        if (short_index == me) {
            shot = true
            if (weapon_name_1 == "ssg 08") {
                Global.ExecuteCommand("slot3");
                flip = true
            }
            if (weapon_name_1 == "awp") {
                Global.ExecuteCommand("slot3");
                flip = true
            }
        } else {
            shot = false
        }

    }
}

function reset_tick() {
    if (flip == true) {
        Global.ExecuteCommand("slot1");
        flip = false
    }
}

//--> Filp swich weapon


//SemiRage assist --> Trigger autowall

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

function autowall() {
    var localPlayer = Entity.GetLocalPlayer()
    tab = getCurrentWeapon(localPlayer);
    const weapon = Entity.GetProp(Entity.GetWeapon(Entity.GetLocalPlayer()), "CBaseAttributableItem", "m_iItemDefinitionIndex") & 0xFFFF;
    if (Cheat.IsRageConfigActive(weapon)) {
    //none
    } else {
       tab = "General";
}
    if (UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Trigger rage autowall"])) {
        var lAWallKey = UI.GetValue(["Config", "SUBTAB_MGR", "Scripts", "SHEET_MGR", "Keys", "JS Keybinds", "Autowall"]);
        if (lAWallKey) {
            UI.SetValue(["Rage", "Target", tab, "Disable autowall"], 0);
        } else {
            UI.SetValue(["Rage", "Target", tab, "Disable autowall"], 1);
        }
    }
};

//SemiRage assist --> Trigger autowall


//Double assist --> DT DMG perdiction

function mindmg() {
    var enemy = Ragebot.GetTarget()
    var startingdmg = Entity.GetProp(enemy, "CCSPlayer", "m_iHealth")
    var dtdmg = startingdmg / 2   
    var shitape = UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "DT DMG perdiction"])
    if (shitape == 1) {
    if (dtdmg == 0) {
        UI.SetValue(["Rage", "Target", "SCAR20", "Minimum damage"], 18)
        UI.SetValue(["Rage", "Target", "G3SG1", "Minimum damage"], 18)
     } else if (dtdmg != 0) {
        UI.SetValue(["Rage", "Target", "SCAR20", "Minimum damage"], dtdmg)
        UI.SetValue(["Rage", "Target", "G3SG1", "Minimum damage"], dtdmg)
    }
  }
}

//Double assist --> DT DMG perdiction


//Double assist --> DT recharge

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

//Double assist --> DT recharge


//--> jump shot

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

//--> jump shot


//--> Slowwalk

function cMove_1() {
    var min = UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Jitter Min"]);
    var max = UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Jitter Max"]);
    var speed = UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Speed"]);
    var fSpeed = UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Forward Speed"]);
    var bSpeed = UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Back Speed"]);
    var sSpeed = UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Side Speed"]);
    var jitteramount = min + Math.floor(Math.random() * (max - min + 1))
    var key = UI.GetValue(["Rage", "Anti Aim", "General", "Key assignment", "Slow walk"]);
    if (key) {
        if (UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Jitter Speed"])) {
            fnspeed = speed + jitteramount
        } else {
            fnspeed = speed
        }

        fnfspeed = fnspeed;
        fnbspeed = fnspeed;
        fnsspeed = fnspeed;

        if (UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Individual speeds"])) {
            if (UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Jitter Speed"])) {
                fnfspeed = fSpeed + jitteramount
                fnbspeed = bSpeed + jitteramount
                fnsspeed = sSpeed + jitteramount
            } else {
                fnfspeed = fSpeed
                fnbspeed = bSpeed
                fnsspeed = sSpeed
            }
        }

        dir = [0, 0, 0];

        if (Input.IsKeyPressed(0x57)) {
            dir[0] += fnfspeed;
        }
        if (Input.IsKeyPressed(0x44)) {
            dir[1] += fnsspeed;
        }
        if (Input.IsKeyPressed(0x41)) {
            dir[1] -= fnsspeed;
        }

        if (Input.IsKeyPressed(0x53)) {
            dir[0] -= fnbspeed;
        }
        UserCMD.SetMovement(dir);
    }
}

//--> Slowwalk


//--> Free camera

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

//--> watermark
var color = UI.GetColor(["Config", "PASTED menu misc.", "PASTED menu misc.", "Watermark color"]);

if (color[3] == 0)
    UI.SetColor(["Config", "PASTED menu misc.", "PASTED menu misc.", "Watermark color"], [250, 164, 22, 255]);

function draw_() {
    if (!World.GetServerString())
        return;
    if (UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Enable menu watermark"])) {
        var today = new Date();
        var hours1 = today.getHours();
        var minutes1 = today.getMinutes();
        var seconds1 = today.getSeconds();

        var hours = hours1 <= 9 ? "0" + hours1 + ":" : hours1 + ":";
        var minutes = minutes1 <= 9 ? "0" + minutes1 + ":" : minutes1 + ":";
        var seconds = seconds1 <= 9 ? "0" + seconds1 : seconds1;

        var server_tickrate = Globals.Tickrate().toString()
        var ebanaya_hueta = Math.round(Entity.GetProp(Entity.GetLocalPlayer(), "CPlayerResource", "m_iPing")).toString()

        color = UI.GetColor(["Config", "PASTED menu misc.", "PASTED menu misc.", "Watermark color"]);

        var font = Render.AddFont("Verdana", 10, 800);
        var text = "CFG By Ye | " + Cheat.GetUsername() + " | delay: " + ebanaya_hueta + "ms | " + server_tickrate + "tick | " + hours + minutes + seconds;

        var w = Render.TextSize(text, font)[0] + 8;
        var x = Global.GetScreenSize()[0];

        x = x - w - 10;

        Render.FilledRect(x, 10, w, 2, [color[0], color[1], color[2], 255]);
        Render.FilledRect(x, 12, w, 16, [17, 17, 17, color[3]]);
        Render.String(x + 3, 10 + 2, 0, text, [255, 255, 255, 255], font);
    }
}


//--> watermark


//--> Hiteffect

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

//--> Hiteffect


//--> pitch set

const groundCounter = 0;
const pitchZeroOnLand = function () {
    if (UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Pitch set"]) == 2) {
        if (!UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Pitch set"]) == 2) return;
        if (!Entity.GetLocalPlayer()) return;

        UI.SetValue(["Cheat", "SHEET_MGR", "General", "Restrictions"], 0);

        const localPlayer = Entity.GetLocalPlayer();
        const localPlayerFlags = Entity.GetProp(localPlayer, "CBasePlayer", "m_fFlags");

        if (localPlayerFlags == 256 || localPlayerFlags == 262) {
            groundCounter = 0;
        }

        if (localPlayerFlags == 257 || localPlayerFlags == 261 || localPlayerFlags == 263) {
            groundCounter = groundCounter + 1;
        }

        if (groundCounter > 10 && groundCounter < 40) {
            UI.SetValue(["Rage", "SUBTAB_MGR", "Anti Aim", "SHEET_MGR", "General", "Pitch mode"], 3);
        } else {
            UI.SetValue(["Rage", "SUBTAB_MGR", "Anti Aim", "SHEET_MGR", "General", "Pitch mode"], 1);
        }
    }

    if (UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Pitch set"]) == 4) {
        UI.SetValue(["Cheat", "SHEET_MGR", "General", "Restrictions"], 0);
        UI.SetValue(["Rage", "SUBTAB_MGR", "Anti Aim", "SHEET_MGR", "General", "Pitch mode"], 6);
    }
    if (UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Pitch set"]) == 3) {
        UI.SetValue(["Cheat", "SHEET_MGR", "General", "Restrictions"], 0);
        UI.SetValue(["Rage", "SUBTAB_MGR", "Anti Aim", "SHEET_MGR", "General", "Pitch mode"], 1);
    }
    if (UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Pitch set"]) == 1) {
        UI.SetValue(["Cheat", "SHEET_MGR", "General", "Restrictions"], 0);
        UI.SetValue(["Rage", "SUBTAB_MGR", "Anti Aim", "SHEET_MGR", "General", "Pitch mode"], 0);
    }
    if (UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Pitch set"]) == 0) {
        UI.SetValue(["Cheat", "SHEET_MGR", "General", "Restrictions"], 0);
    }

}

//--> pitch set


//--> Bullet Tracer

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

//--> Bullet Tracer


//--> Grandes radius

var smoke = [];
const smokeStart = function () {
    entity = Event.GetInt("entityid");
    x = Event.GetFloat("x");
    y = Event.GetFloat("y");
    z = Event.GetFloat("z");
    smoke.push({
        entity: entity,
        position: [x, y, z]
    });
}
const smokeExpire = function () {
    for (var i = 0; i < smoke.length; i++) {
        if (smoke[i].entity == Event.GetInt("entityid")) {
            smoke.splice(i, 1);
        }
    }
}
const smokeDraw = function () {
    if (!UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Enable smoke radius"])) return;
    for (var i = 0; i < smoke.length; i++) {
        vecOrigin = smoke[i].position;
        const lineColor = UI.GetColor(["Config", "PASTED menu misc.", "PASTED menu misc.", "Smoke line color"]);
        const radiusColor = UI.GetColor(["Config", "PASTED menu misc.", "PASTED menu misc.", "Smoke radius color"]);
        draw_circle_3d(vecOrigin[0], vecOrigin[1], vecOrigin[2], 160, 360, 0, [lineColor[0], lineColor[1], lineColor[2], lineColor[3]], [radiusColor[0], radiusColor[1], radiusColor[2], radiusColor[3]]);
    }
}
const onDraw = function () {
    smokeDraw();
}
const clearData = function () {
    for (var i = 0; i < smoke.length; i++) {
        smoke.splice(i, 1);
    }
}

//--> Grandes radius


//--> Other misc.

var orgaspect = Convar.GetFloat("r_aspectratio");
var clhc = Convar.GetInt("cl_hud_color");
var colour = 1;
var time = Globals.Curtime();

function aspect() {
    if (UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Enable Aspect Ratio Changer"])) {
        uiaspect = UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Aspect Ratio"]);
        Convar.SetFloat("r_aspectratio", uiaspect);
    } else {
        Convar.SetFloat("r_aspectratio", orgaspect);
    }
}
var pswitch = false;

function rainbow() {
    if (UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Enable Rainow HUD"])) {
        Convar.SetInt("cl_hud_color", colour);
        if (Globals.Curtime() - UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Colour Switch Speed"]) >= time) {
            colour = colour + 1
            time = Globals.Curtime()
        }
        if (colour > 9) {
            colour = 1
        }
    }
}
var currentTick = 0;
var lastTick = 0;
var speed = 10;
var ctag = 0
var tag = "";
var slc = 0;

function cttoleftscroll(inputct) {
    var arr = [];
    var str = inputct;
    var length = str.length;
    var i = 0;
    while (true) {
        if (i > length) {
            break;
        }
        if (i < 2) {
            arr.push(str.slice(i, length));
        } else {
            arr.push(str.slice(i, length) + str.slice(0, i - 1));
        }
        i = i + 1
    }
    return (arr)
}

function cttorightscroll(inputct) {
    var arr = [];
    var str = inputct;
    var length = str.length;
    var i = 0;
    while (true) {
        if (i > length) {
            break;
        }
        if (i < 1) {
            arr.push(str.slice(0, length));
        } else {
            arr.push(str.slice(length - i, length) + str.slice(0, length - i));
        }
        i = i + 1
    }
    return (arr)
}

function cttolefttype(inputct) {
    var arr = [];
    var str = inputct;
    var length = str.length;
    var i = 0;
    var ii = length - 1;
    while (true) {
        if (i >= length + 1) {
            arr.push(str.slice(0, length - ii));
            ii = ii - 1;
            if (ii == 0) {
                break;
            }
        } else {
            arr.push(str.slice(0, length - i));
            i = i + 1;
        }
    }
    return (arr)
}

function cttorighttype(inputct) {
    var arr = [];
    var str = inputct;
    var length = str.length;
    var i = 0;
    var ii = length - 1;
    while (true) {
        if (i >= length + 1) {
            arr.push(str.slice(ii, length));
            ii = ii - 1;
            if (ii == 0) {
                arr.push(str);
                arr.push(str);
                break;
            }
        } else {
            arr.push(str.slice(i, length));
            i = i + 1;
        }
    }
    return (arr)
}

function Ct() {

    if (UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Enable Clantag Changer"])) {
        if (UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Clantag"]) == 1) {
            tag = "OneTap.com ";
        } else if (UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Clantag"]) == 2) {
            tag = "CFG By Ye ";
        } else if (UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Clantag"]) == 3) {
            tag = UI.GetString(["Config", "PASTED menu misc.", "PASTED menu misc.", "Custom Clantag"]);
        } else {
            tag = "";
        }
        currentTick = parseInt(Globals.Curtime() * 1000);
        if (currentTick - (10000 / UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Clantag Speed"])) >= lastTick) {
            if (tag.length < 17) {
                if (UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Clantag Animation"]) == 0 || UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Clantag Animation"]) == 1 || UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Clantag"]) == 0) {
                    switch ((ctag) % 2) {
                        case 0:
                            {
                                Local.SetClanTag(tag);
                                break;
                            }
                        case 1:
                            {
                                if (!UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Clantag Animation"]) == 0) {
                                    Local.SetClanTag("");
                                }
                                break;
                            }
                    }
                    if (ctag == 1) {
                        ctag = 0;
                    } else {
                        ctag = ctag + 1;
                    }
                    lastTick = currentTick;
                } else {
                    if (tag.length > 3) {
                        if (UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Clantag Animation"]) == 2) {
                            var ctarray = cttoleftscroll(tag)
                        } else if (UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Clantag Animation"]) == 3) {
                            var ctarray = cttorightscroll(tag)
                        } else if (UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Clantag Animation"]) == 4) {
                            var ctarray = cttolefttype(tag)
                        } else {
                            var ctarray = cttorighttype(tag)
                        }

                        Local.SetClanTag(ctarray[slc]);

                        if (slc == ctarray.length - 1) {
                            slc = 0
                        } else {
                            slc = slc + 1
                        }
                        lastTick = currentTick;
                    }
                }
            }
        }
    }
}

//--> Other misc.


//--> mm fake duck
var shot = false
Render.OutlinedString = function (c, d, e, f, g, h, i) {
    Render.String(c - 0x1, d, e, f, [0x0, 0x0, 0x0, i], h);
    Render.String(c + 0x1, d, e, f, [0x0, 0x0, 0x0, i], h);
    Render.String(c, d - 0x1, e, f, [0x0, 0x0, 0x0, i], h);
    Render.String(c, d + 0x1, e, f, [0x0, 0x0, 0x0, i], h);
    Render.String(c, d, e, f, [g[0x0], g[0x1], g[0x2], i], h)
}
var max_level = 50;

function indicator() {
    const c = Entity.GetLocalPlayer();
    const d = Entity.IsAlive(c);
    var is_valve_server = Entity.GetProp(Entity.GetGameRulesProxy(), "CCSGameRulesProxy", "m_bIsValveDS");
    if (is_valve_server && d) {
        if (UI.GetValue(["Config", "MM fakeduck", "MM fakeduck", "[FD] Height prediction"]) && UI.GetValue(["Config", "SUBTAB_MGR", "Scripts", "SHEET_MGR", "Keys", "JS Keybinds", "[FD]Keybind"]) && UI.GetValue(["Misc.", "Keys", "General", "Key assignment", "Thirdperson"]) == 1) {
            var e = Entity.GetEyePosition(c);
            const f = Entity.GetRenderOrigin(c);
            e[2] = f[2] + 46 + (18 - (max_level + 1) / 100 * 18);
            const g = Render.WorldToScreen(e);
            Render.FilledCircle(g[0] + 1, g[1], 7, [0, 0, 0, 150]);
            Render.Circle(g[0] + 1, g[1], 7, [255, 255, 255, 255])
        }

        if (UI.GetValue(["Config", "MM fakeduck", "MM fakeduck", "[FD] Indicator"])) {
            const h = Render.AddFont("Arial", 24, 100);
            Render.OutlinedString(100, Render.GetScreenSize()[1] / 2, 0, "[FD] Level" + ' ' + max_level, [255, 255, 255, 255], h, 255)
        }
    }
}
var crouched = false;
auth_ok = function () {
    var buttons = UserCMD.GetButtons()
    UserCMD.SetButtons(buttons | (1 << 22))
    var c = UserCMD.GetButtons();
    const d = Entity.GetLocalPlayer();
    const e = Entity.IsAlive(d);
    var is_valve_server = Entity.GetProp(Entity.GetGameRulesProxy(), "CCSGameRulesProxy", "m_bIsValveDS");

    const f = UI.GetValue(["Config", "MM fakeduck", "MM fakeduck", "[FD] Presets"]);
    if (f == 0) {
        UI.SetEnabled(["Config", "MM fakeduck", "MM fakeduck", "[FD] Preset 1"], 1);
        UI.SetEnabled(["Config", "MM fakeduck", "MM fakeduck", "[FD] Preset 2"], 0);
        UI.SetEnabled(["Config", "MM fakeduck", "MM fakeduck", "[FD] Preset 3"], 0);
        UI.SetEnabled(["Config", "MM fakeduck", "MM fakeduck", "[FD] Preset 4"], 0);
    }
    if (f == 1) {
        UI.SetEnabled(["Config", "MM fakeduck", "MM fakeduck", "[FD] Preset 1"], 0);
        UI.SetEnabled(["Config", "MM fakeduck", "MM fakeduck", "[FD] Preset 2"], 1);
        UI.SetEnabled(["Config", "MM fakeduck", "MM fakeduck", "[FD] Preset 3"], 0);
        UI.SetEnabled(["Config", "MM fakeduck", "MM fakeduck", "[FD] Preset 4"], 0);
    }
    if (f == 2) {
        UI.SetEnabled(["Config", "MM fakeduck", "MM fakeduck", "[FD] Preset 1"], 0);
        UI.SetEnabled(["Config", "MM fakeduck", "MM fakeduck", "[FD] Preset 2"], 0);
        UI.SetEnabled(["Config", "MM fakeduck", "MM fakeduck", "[FD] Preset 3"], 1);
        UI.SetEnabled(["Config", "MM fakeduck", "MM fakeduck", "[FD] Preset 4"], 0);
    }
    if (f == 3) {
        UI.SetEnabled(["Config", "MM fakeduck", "MM fakeduck", "[FD] Preset 1"], 0);
        UI.SetEnabled(["Config", "MM fakeduck", "MM fakeduck", "[FD] Preset 2"], 0);
        UI.SetEnabled(["Config", "MM fakeduck", "MM fakeduck", "[FD] Preset 3"], 0);
        UI.SetEnabled(["Config", "MM fakeduck", "MM fakeduck", "[FD] Preset 4"], 1);
    }
    var leveal = Math.floor(Math.random() * (5 - 1) + 1);
    max_level = UI.GetValue(["Config", "MM fakeduck", "MM fakeduck", "[FD] Preset " + leveal]);
    var g = Entity.GetProp(d, "CCSPlayer", "m_flDuckAmount");
    if (UI.GetValue(["Config", "SUBTAB_MGR", "Scripts", "SHEET_MGR", "Keys", "JS Keybinds", "[FD]Keybind"]) && is_valve_server && e) {
      UI.SetValue(["Rage", "Fake Lag", "Limit"], 16);
      UI.SetValue(["Rage", "Fake Lag", "Trigger limit"], 16);
      UI.SetValue(["Rage", "Fake Lag", "Jitter"], 0);
        if (shot) {
            UserCMD.Send();
        }else{
            UserCMD.Choke();
        };
        if (g <= max_level / 100) {
            crouched = true
        };
        if (g >= 0.78) {
            crouched = false;
        };
        var h = 1 << 2;
        crouched ? c |= h : c &= ~h;
        UserCMD.SetButtons(c | 1 << 22);
    }
};

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


//ui
UI.AddSubTab(["Config", "SUBTAB_MGR"], "MM fakeduck")
UI.AddSliderInt(["Config", "MM fakeduck", "MM fakeduck"], "--Fix. byPASTED--", 0, 0);
UI.AddHotkey(["Config", "SUBTAB_MGR", "Scripts", "SHEET_MGR", "Keys", "JS Keybinds"], "[FD]Keybind", "MM Fake Duck");
UI.AddCheckbox(["Config", "MM fakeduck", "MM fakeduck"], "[FD] Indicator");
UI.AddCheckbox(["Config", "MM fakeduck", "MM fakeduck"], "[FD] Height prediction");
UI.AddDropdown(["Config", "MM fakeduck", "MM fakeduck"], "[FD] On shot command", ["Default", "Send", "Choke"], 0);
UI.AddDropdown(["Config", "MM fakeduck", "MM fakeduck"], "[FD] Presets", ["Preset 1", "Preset 2", "Preset 3", "Preset 4"], 0);
UI.AddSliderInt(["Config", "MM fakeduck", "MM fakeduck"], "[FD] Preset 1", 0, 100);
UI.AddSliderInt(["Config", "MM fakeduck", "MM fakeduck"], "[FD] Preset 2", 0, 100);
UI.AddSliderInt(["Config", "MM fakeduck", "MM fakeduck"], "[FD] Preset 3", 0, 100);
UI.AddSliderInt(["Config", "MM fakeduck", "MM fakeduck"], "[FD] Preset 4", 0, 100);
//ui

function ragebot_fire() {
    const c = UI.GetValue(["Config", "MM fakeduck", "MM fakeduck", "[FD] On shot command"]);
    switch (c) {
        default: break;
        case 0x1:
            UserCMD.Send();
            break;
        case 0x2:
            UserCMD.Choke();
            break;
    }
}

//--> mm fake duck


//menu设定开始----------------------------------------------------------------------                                                  
UI.AddSubTab(["Config", "SUBTAB_MGR"], "Anti-Aim++");
UI.AddDropdown(["Config", "Anti-Aim++", "Anti-Aim++"], "AA mode", ["Default", "Sway AA", "Custom AA", "Advanced sway AA",], 0);
UI.AddCheckbox(["Config", "Anti-Aim++", "Anti-Aim++"], "Yaw & jitter");
UI.AddCheckbox(["Config", "Anti-Aim++", "Anti-Aim++"], "Fakelag & Anti-Brute");

//AA mode 1 "sway AA"
UI.AddSliderInt(["Config", "Anti-Aim++", "Anti-Aim++"], "--Sway AA--", 0, 0);
//UI.AddLabel("=========Real Sway=========");
UI.AddSliderInt(["Config", "Anti-Aim++", "Anti-Aim++"], "--Real Sway--", 0, 0);
UI.AddSliderInt(["Config", "Anti-Aim++", "Anti-Aim++"], "Real Sway Angle A", -65, 65);
UI.AddSliderInt(["Config", "Anti-Aim++", "Anti-Aim++"], "Real Sway Angle B", -65, 65);
UI.AddSliderInt(["Config", "Anti-Aim++", "Anti-Aim++"], "Real Sway Speed", 0, 10);

//UI.AddLabel("=========LBY Sway=========");
UI.AddSliderInt(["Config", "Anti-Aim++", "Anti-Aim++"], "--LBY Sway--", 0, 0);
UI.AddSliderInt(["Config", "Anti-Aim++", "Anti-Aim++"], "LBY Sway Angle A", -55, 55);
UI.AddSliderInt(["Config", "Anti-Aim++", "Anti-Aim++"], "LBY Sway Angle B", -55, 55);
UI.AddSliderInt(["Config", "Anti-Aim++", "Anti-Aim++"], "LBY Sway Speed", 0, 5);

//AA mode 2 "custom AA"
UI.AddSliderInt(["Config", "Anti-Aim++", "Anti-Aim++"], "--Custom AA--", 0, 0);
UI.AddSliderInt(["Config", "Anti-Aim++", "Anti-Aim++"], "LBY Delta", 0, 60)
UI.AddSliderInt(["Config", "Anti-Aim++", "Anti-Aim++"], "Real Delta", -60, 0)
UI.AddSliderInt(["Config", "Anti-Aim++", "Anti-Aim++"], "Inverted LBY Delta", -60, 0)
UI.AddSliderInt(["Config", "Anti-Aim++", "Anti-Aim++"], "Inverted Real Delta", 0, 60)

//AA mode 3 "Advanced sway AA"
UI.AddHotkey(["Rage", "Anti Aim", "General", "Key assignment"], "Tank Walk", "Tank Walk");
UI.AddSliderInt(["Config", "Anti-Aim++", "Anti-Aim++"], "Speed:", 0, 135);
UI.AddCheckbox(["Config", "Anti-Aim++", "Anti-Aim++"], "Advanced Jitter");
UI.AddSliderInt(["Config", "Anti-Aim++", "Anti-Aim++"], "Jitter limit", -180, 180);
UI.AddCheckbox(["Config", "Anti-Aim++", "Anti-Aim++"], "Offset Break");
UI.AddCheckbox(["Config", "Anti-Aim++", "Anti-Aim++"], "Freestand On Hit");
UI.AddSliderFloat(["Config", "Anti-Aim++", "Anti-Aim++"], "Freestand Duration", 0, 5);
UI.AddCheckbox(["Config", "Anti-Aim++", "Anti-Aim++"], "AA-Swing");
UI.AddCheckbox(["Config", "Anti-Aim++", "Anti-Aim++"], "Swing astrict");
UI.AddSliderInt(["Config", "Anti-Aim++", "Anti-Aim++"], "Sway Amount", 0, 60);
UI.AddSliderInt(["Config", "Anti-Aim++", "Anti-Aim++"], "Sway Range", 0, 360);
UI.AddSliderInt(["Config", "Anti-Aim++", "Anti-Aim++"], "Sway frequency", 1, 50);
UI.AddCheckbox(["Config", "Anti-Aim++", "Anti-Aim++"], "False jitter");
UI.AddSliderInt(["Config", "Anti-Aim++", "Anti-Aim++"], "False jitter Speed", 1, 100);
UI.AddSliderInt(["Config", "Anti-Aim++", "Anti-Aim++"], "False jitter Range", 1, 100);
UI.AddSliderInt(["Config", "Anti-Aim++", "Anti-Aim++"], "False jitter Step", 1, 10);
UI.AddCheckbox(["Config", "Anti-Aim++", "Anti-Aim++"], "AntiAim-Switch");
UI.AddSliderInt(["Config", "Anti-Aim++", "Anti-Aim++"], "Switch Delay", 1, 1000);
UI.AddSliderInt(["Config", "Anti-Aim++", "Anti-Aim++"], "Switch Yaw - A", -180, 180);
UI.AddSliderInt(["Config", "Anti-Aim++", "Anti-Aim++"], "Switch Yaw - B", -180, 180);
UI.AddSliderInt(["Config", "Anti-Aim++", "Anti-Aim++"], "Switch Yaw - C", -180, 180);

//UI.AddLabel("=======Yaw & Jitter=======");
UI.AddSliderInt(["Config", "Anti-Aim++", "Anti-Aim++"], "--Yaw & Jitter--", 0, 0);
UI.AddSliderInt(["Config", "Anti-Aim++", "Anti-Aim++"], "Yaw & Jitter", -180, 180);
UI.AddCheckbox(["Config", "Anti-Aim++", "Anti-Aim++"], "Random Yaw & Jitter");
UI.AddSliderInt(["Config", "Anti-Aim++", "Anti-Aim++"], "Random jitter speed", 0, 5);
UI.AddSliderInt(["Config", "Anti-Aim++", "Anti-Aim++"], "Fake Offset", -55, 55);
UI.AddCheckbox(["Config", "Anti-Aim++", "Anti-Aim++"], "Random Fake Offset");

//UI.AddLabel("=======FakeLag=======");
UI.AddSliderInt(["Config", "Anti-Aim++", "Anti-Aim++"], "--FakeLag--", 0, 0);
UI.AddSliderInt(["Config", "Anti-Aim++", "Anti-Aim++"], "Fakelag Max", 0, 16);
UI.AddSliderInt(["Config", "Anti-Aim++", "Anti-Aim++"], "Fakelag Min", 0, 16);
UI.AddSliderInt(["Config", "Anti-Aim++", "Anti-Aim++"], "Fakelag Delay", 0, 200);
UI.AddSliderInt(["Config", "Anti-Aim++", "Anti-Aim++"], "Trigger fakelag Max", 0, 16);
UI.AddSliderInt(["Config", "Anti-Aim++", "Anti-Aim++"], "Trigger fakelag Min", 0, 16);
UI.AddSliderInt(["Config", "Anti-Aim++", "Anti-Aim++"], "Trigger fakelag Delay", 0, 200);
UI.AddSliderInt(["Config", "Anti-Aim++", "Anti-Aim++"], "Fakelag jitter Max", 0, 100);
UI.AddSliderInt(["Config", "Anti-Aim++", "Anti-Aim++"], "Fakelag jitter Min", 0, 100);
UI.AddSliderInt(["Config", "Anti-Aim++", "Anti-Aim++"], "Fakelag jitter Delay", 0, 200);
UI.AddCheckbox(["Config", "Anti-Aim++", "Anti-Aim++"], "FakeLag On Move");
UI.AddSliderInt(["Config", "Anti-Aim++", "Anti-Aim++"], "Move Fakelag", 0, 16);
UI.AddCheckbox(["Config", "Anti-Aim++", "Anti-Aim++"], "Fakelag On Auto Stop");
UI.AddSliderInt(["Config", "Anti-Aim++", "Anti-Aim++"], "Auto Stop Fakelag", 0, 16);

//UI.AddLabel("=======Anti-Brute=======");
UI.AddSliderInt(["Config", "Anti-Aim++", "Anti-Aim++"], "--Anti-Brute--", 0, 0);
UI.AddCheckbox(["Config", "Anti-Aim++", "Anti-Aim++"], "On shot mode");
UI.AddSliderInt(["Config", "Anti-Aim++", "Anti-Aim++"], "On shot fakelag", 0, 16);
UI.AddCheckbox(["Config", "Anti-Aim++", "Anti-Aim++"], "Dynamic desync on shot");
UI.AddCheckbox(["Config", "Anti-Aim++", "Anti-Aim++"], "Break leg");
UI.AddDropdown(["Config", "Anti-Aim++", "Anti-Aim++"], "Anti Bruteforce", ["Off", "On Hit", "On Shot"], 0);
//UI.AddLabel("=========PASTED anti-aim=========");

//UI可见性------------------------- ---------------------------------------------

function UIEnabled() {

    if (UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "AA mode"]) == 0) {
        AntiAim.SetOverride(0);
    }
    if (UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "AA indicator"])) {
        UI.SetEnabled(["Config", "PASTED menu misc.", "PASTED menu misc.", "AA indicator mode"], 1);
    } else {
        UI.SetEnabled(["Config", "PASTED menu misc.", "PASTED menu misc.", "AA indicator mode"], 0);
    }

    if (UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Enable menu watermark"])) {
        UI.SetEnabled(["Config", "PASTED menu misc.", "PASTED menu misc.", "Watermark color"], 1);
    } else {
        UI.SetEnabled(["Config", "PASTED menu misc.", "PASTED menu misc.", "Watermark color"], 0);
    }

    if (UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Menu indicator"])) {
        UI.SetEnabled(["Config", "PASTED menu misc.", "PASTED menu misc.", "AA indicator"], 1);
        UI.SetEnabled(["Config", "PASTED menu misc.", "PASTED menu misc.", "Enable C4 Indicator"], 1);
        UI.SetEnabled(["Config", "PASTED menu misc.", "PASTED menu misc.", "Crosshair hitmarker"], 1);
        UI.SetEnabled(["Config", "PASTED menu misc.", "PASTED menu misc.", "Crosshair Dmg log"], 1);
        UI.SetEnabled(["Config", "PASTED menu misc.", "PASTED menu misc.", "Bar text indicator"], 1);
        UI.SetEnabled(["Config", "PASTED menu misc.", "PASTED menu misc.", "Health bar indicator"], 1);
        UI.SetEnabled(["Config", "PASTED menu misc.", "PASTED menu misc.", "Top RGB line"], 1);
    } else {
        UI.SetEnabled(["Config", "PASTED menu misc.", "PASTED menu misc.", "AA indicator"], 0);
        UI.SetEnabled(["Config", "PASTED menu misc.", "PASTED menu misc.", "Enable C4 Indicator"], 0);
        UI.SetEnabled(["Config", "PASTED menu misc.", "PASTED menu misc.", "Crosshair hitmarker"], 0);
        UI.SetEnabled(["Config", "PASTED menu misc.", "PASTED menu misc.", "Crosshair Dmg log"], 0);
        UI.SetEnabled(["Config", "PASTED menu misc.", "PASTED menu misc.", "Bar text indicator"], 0);
        UI.SetEnabled(["Config", "PASTED menu misc.", "PASTED menu misc.", "Health bar indicator"], 0);
        UI.SetEnabled(["Config", "PASTED menu misc.", "PASTED menu misc.", "Top RGB line"], 0);
    }
    if (UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Enable free camera"])){
        UI.SetEnabled(["Config", "PASTED menu misc.", "PASTED menu misc.", "Max free camera follow value"], 1);
    }else{
        UI.SetEnabled(["Config", "PASTED menu misc.", "PASTED menu misc.", "Max free camera follow value"], 0);
    }

    if (UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Jump Scout/Revolver Hitchance"])) {
        UI.SetEnabled(["Config", "PASTED menu misc.", "PASTED menu misc.", "Hitchance"], 1)
    } else {
        UI.SetEnabled(["Config", "PASTED menu misc.", "PASTED menu misc.", "Hitchance"], 0)
    }
    var min = UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Jitter Min"]);
    var max = UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Jitter Max"]);
    if (min > max) {
        UI.SetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Jitter Max"], min);
    }
    if (max < min) {
        UI.SetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Jitter Min"], max);
    }
    UI.SetEnabled(["Config", "PASTED menu misc.", "PASTED menu misc.", "Forward Speed"], 0);
    UI.SetEnabled(["Config", "PASTED menu misc.", "PASTED menu misc.", "Side Speed"], 0);
    UI.SetEnabled(["Config", "PASTED menu misc.", "PASTED menu misc.", "Back Speed"], 0);
    UI.SetEnabled(["Config", "PASTED menu misc.", "PASTED menu misc.", "Jitter Min"], 0);
    UI.SetEnabled(["Config", "PASTED menu misc.", "PASTED menu misc.", "Jitter Max"], 0);
    if (UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Individual speeds"])) {
        UI.SetEnabled(["Config", "PASTED menu misc.", "PASTED menu misc.", "Forward Speed"], 1);
        UI.SetEnabled(["Config", "PASTED menu misc.", "PASTED menu misc.", "Side Speed"], 1);
        UI.SetEnabled(["Config", "PASTED menu misc.", "PASTED menu misc.", "Back Speed"], 1);
    }

    if (UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Jitter Speed"])) {
        UI.SetEnabled(["Config", "PASTED menu misc.", "PASTED menu misc.", "Jitter Min"], 1);
        UI.SetEnabled(["Config", "PASTED menu misc.", "PASTED menu misc.", "Jitter Max"], 1);

    }
    if (UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Log in chat"])) {
        UI.SetEnabled(["Config", "PASTED menu misc.", "PASTED menu misc.", "Buy Logs"], 1);
        UI.SetEnabled(["Config", "PASTED menu misc.", "PASTED menu misc.", "Dmg Logs"], 1);
        UI.SetEnabled(["Config", "PASTED menu misc.", "PASTED menu misc.", "Vote Logs"], 1);
    } else {
        UI.SetEnabled(["Config", "PASTED menu misc.", "PASTED menu misc.", "Buy Logs"], 0);
        UI.SetEnabled(["Config", "PASTED menu misc.", "PASTED menu misc.", "Dmg Logs"], 0);
        UI.SetEnabled(["Config", "PASTED menu misc.", "PASTED menu misc.", "Vote Logs"], 0);
    }

    if (UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "SemiRage assist"])) {
        UI.SetEnabled(["Config", "PASTED menu misc.", "PASTED menu misc.", "Trigger rage autowall"], 1);
    } else {
        UI.SetEnabled(["Config", "PASTED menu misc.", "PASTED menu misc.", "Trigger rage autowall"], 0);
    }

    if (UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Double Tap assist"])) {
        UI.SetEnabled(["Config", "PASTED menu misc.", "PASTED menu misc.", "DT DMG perdiction"], 1);
        UI.SetEnabled(["Config", "PASTED menu misc.", "PASTED menu misc.", "Better DT recharge"], 1);
    } else {
        UI.SetEnabled(["Config", "PASTED menu misc.", "PASTED menu misc.", "DT DMG perdiction"], 0);
        UI.SetEnabled(["Config", "PASTED menu misc.", "PASTED menu misc.", "Better DT recharge"], 0);
    }

    if (UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Show Bullet Tracer"])) {
        UI.SetEnabled(["Config", "PASTED menu misc.", "PASTED menu misc.", "Bullet Tracer Thickness"], 1);
        UI.SetEnabled(["Config", "PASTED menu misc.", "PASTED menu misc.", "Bullet Tracer Color"], 1);
        UI.SetEnabled(["Config", "PASTED menu misc.", "PASTED menu misc.", "RGB Tracer Color"], 1);
    } else {
        UI.SetEnabled(["Config", "PASTED menu misc.", "PASTED menu misc.", "Bullet Tracer Thickness"], 0);
        UI.SetEnabled(["Config", "PASTED menu misc.", "PASTED menu misc.", "Bullet Tracer Color"], 0);
        UI.SetEnabled(["Config", "PASTED menu misc.", "PASTED menu misc.", "RGB Tracer Color"], 0);
    }

    if (UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Enable smoke radius"])) {
        UI.SetEnabled(["Config", "PASTED menu misc.", "PASTED menu misc.", "Smoke radius color"], 1);
        UI.SetEnabled(["Config", "PASTED menu misc.", "PASTED menu misc.", "Smoke line color"], 1);
    } else {
        UI.SetEnabled(["Config", "PASTED menu misc.", "PASTED menu misc.", "Smoke radius color"], 0);
        UI.SetEnabled(["Config", "PASTED menu misc.", "PASTED menu misc.", "Smoke line color"], 0);
    }

    if (UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Enable Rainow HUD"])) {
        UI.SetEnabled(["Config", "PASTED menu misc.", "PASTED menu misc.", "Colour Switch Speed"], 1);
    } else {
        UI.SetEnabled(["Config", "PASTED menu misc.", "PASTED menu misc.", "Colour Switch Speed"], 0);
    }
    if (UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Enable Clantag Changer"])) {
        UI.SetEnabled(["Config", "PASTED menu misc.", "PASTED menu misc.", "Clantag"], 1);
        UI.SetEnabled(["Config", "PASTED menu misc.", "PASTED menu misc.", "Clantag Animation"], 1);
        UI.SetEnabled(["Config", "PASTED menu misc.", "PASTED menu misc.", "Clantag Speed"], 1);
        UI.SetEnabled(["Config", "PASTED menu misc.", "PASTED menu misc.", "Custom Clantag"], 1);
    } else {
        UI.SetEnabled(["Config", "PASTED menu misc.", "PASTED menu misc.", "Clantag"], 0);
        UI.SetEnabled(["Config", "PASTED menu misc.", "PASTED menu misc.", "Clantag Animation"], 0);
        UI.SetEnabled(["Config", "PASTED menu misc.", "PASTED menu misc.", "Clantag Speed"], 0);
        UI.SetEnabled(["Config", "PASTED menu misc.", "PASTED menu misc.", "Custom Clantag"], 0);
    }

    if (UI.GetValue(["Config", "PASTED menu misc.", "PASTED menu misc.", "Enable Aspect Ratio Changer"])) {
        UI.SetEnabled(["Config", "PASTED menu misc.", "PASTED menu misc.", "Aspect Ratio"], 1);
    } else {
        UI.SetEnabled(["Config", "PASTED menu misc.", "PASTED menu misc.", "Aspect Ratio"], 0);
    }

    // sway AA enable
    if (UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "AA mode"]) == 1) {
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "--Sway AA--"], 1);
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "--Real Sway--"], 1);
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Real Sway Angle A"], 1);
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Real Sway Angle B"], 1);
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Real Sway Speed"], 1);
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "--LBY Sway--"], 1);
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "LBY Sway Angle A"], 1);
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "LBY Sway Angle B"], 1);
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "LBY Sway Speed"], 1);
    } else {
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "--Sway AA--"], 0);
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "--Real Sway--"], 0);
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Real Sway Angle A"], 0);
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Real Sway Angle B"], 0);
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Real Sway Speed"], 0);
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "--LBY Sway--"], 0);
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "LBY Sway Angle A"], 0);
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "LBY Sway Angle B"], 0);
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "LBY Sway Speed"], 0);
    }

    //custom AA
    if (UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "AA mode"]) == 2) {
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "--Custom AA--"], 1);;
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "LBY Delta"], 1);
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Real Delta"], 1);
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Inverted LBY Delta"], 1);;
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Inverted Real Delta"], 1);;
    } else {
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "--Custom AA--"], 0);
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "LBY Delta"], 0);
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Real Delta"], 0);
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Inverted LBY Delta"], 0);
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Inverted Real Delta"], 0);
    }

    //Advanced sway AA
    if (UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "AA mode"]) == 3) {
        UI.SetValue(["Config", "Anti-Aim++", "Anti-Aim++", "Yaw & jitter"], 0)
        UI.SetEnabled(["Rage", "Anti Aim", "General", "Key assignment", "Tank Walk"], 1);
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Speed:"], 1)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Advanced Jitter"], 1)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Jitter limit"], 1)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Offset Break"], 1)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Speed:"], 1)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Advanced Jitter"], 1)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Jitter limit"], 1)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Offset Break"], 1)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Freestand On Hit"], 1)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Freestand Duration"], 1)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "AA-Swing"], 1)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Swing astrict"], 1)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Sway Amount"], 1)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Sway Range"], 1)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Sway frequency"], 1)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "False jitter"], 1)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "False jitter Speed"], 1)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "False jitter Range"], 1)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "False jitter Step"], 1)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "AntiAim-Switch"], 1)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Switch Delay"], 1)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Switch Yaw - A"], 1)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Switch Yaw - B"], 1)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Switch Yaw - C"], 1)
    } else {
        UI.SetEnabled(["Rage", "Anti Aim", "General", "Key assignment", "Tank Walk"], 0);
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Speed:"], 0)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Advanced Jitter"], 0)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Jitter limit"], 0)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Offset Break"], 0)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Speed:"], 0)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Advanced Jitter"], 0)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Jitter limit"], 0)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Offset Break"], 0)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Freestand On Hit"], 0)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Freestand Duration"], 0)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "AA-Swing"], 0)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Swing astrict"], 0)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Sway Amount"], 0)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Sway Range"], 0)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Sway frequency"], 0)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "False jitter"], 0)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "False jitter Speed"], 0)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "False jitter Range"], 0)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "False jitter Step"], 0)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "AntiAim-Switch"], 0)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Switch Delay"], 0)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Switch Yaw - A"], 0)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Switch Yaw - B"], 0)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Switch Yaw - C"], 0)
    }

    if (UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "Yaw & jitter"])) {
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "--Yaw & Jitter--"], 1)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Random jitter speed"], 1)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Yaw & Jitter"], 1)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Random Yaw & Jitter"], 1)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Fake Offset"], 1)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Random Fake Offset"], 1)
    } else {
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "--Yaw & Jitter--"], 0)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Random jitter speed"], 0)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Yaw & Jitter"], 0)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Random Yaw & Jitter"], 0)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Fake Offset"], 0)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Random Fake Offset"], 0)
    }

    if (UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "Fakelag & Anti-Brute"])) {
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "--FakeLag--"], 1)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Fakelag Max"], 1)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Fakelag Min"], 1)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Fakelag Delay"], 1)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Trigger fakelag Max"], 1)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Trigger fakelag Min"], 1)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Trigger fakelag Delay"], 1)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Fakelag jitter Max"], 1)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Fakelag jitter Min"], 1)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Fakelag jitter Delay"], 1)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "FakeLag On Move"], 1)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Move Fakelag"], 1);
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Fakelag On Auto Stop"], 1)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Auto Stop Fakelag"], 1);
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "--Anti-Brute--"], 1)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "On shot mode"], 1)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Break leg"], 1)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Anti Bruteforce"], 1)
    } else {
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Move Fakelag"], 0);
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Auto Stop Fakelag"], 0);
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "--FakeLag--"], 0)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Fakelag Max"], 0)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Fakelag Min"], 0)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Fakelag Delay"], 0)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Trigger fakelag Max"], 0)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Trigger fakelag Min"], 0)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Trigger fakelag Delay"], 0)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Fakelag jitter Max"], 0)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Fakelag jitter Min"], 0)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Fakelag jitter Delay"], 0)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "FakeLag On Move"], 0);
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Fakelag On Auto Stop"], 0);
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "--Anti-Brute--"], 0)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "On shot mode"], 0)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Break leg"], 0)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Anti Bruteforce"], 0)
    }
    if (UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "Fakelag Max"]) < UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "Fakelag Min"])) {
        UI.SetValue(["Config", "Anti-Aim++", "Anti-Aim++", "Fakelag Min"], UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "Fakelag Max"]))
    }
    if (UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "Trigger fakelag Max"]) < UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "Trigger fakelag Min"])) {
        UI.SetValue(["Config", "Anti-Aim++", "Anti-Aim++", "Trigger fakelag Min"], UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "Trigger fakelag Max"]))
    }
    if (UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "Fakelag jitter Max"]) < UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "Fakelag jitter Min"])) {
        UI.SetValue(["Config", "Anti-Aim++", "Anti-Aim++", "Fakelag jitter Min"], UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "Fakelag jitter Max"]))
    }

    //fakelag on move
    if (UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "FakeLag On Move"])) {
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Move Fakelag"], 1);
    } else {
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Move Fakelag"], 0);
    }
    //fakelag on autostop
    if (UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "Fakelag On Auto Stop"])) {
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Auto Stop Fakelag"], 1)
    } else {
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Auto Stop Fakelag"], 0)
    }

    if (UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "On shot mode"])) {
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "On shot fakelag"], 1)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Dynamic desync on shot"], 1)
    } else {
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "On shot fakelag"], 0)
        UI.SetEnabled(["Config", "Anti-Aim++", "Anti-Aim++", "Dynamic desync on shot"], 0)
    }

    if (UI.GetValue(["Config", "[PASTED]Freestanding", "[PASTED]Freestanding", "Enable freestanding"])) {
        UI.SetEnabled(["Config", "[PASTED]Freestanding", "[PASTED]Freestanding", "Freestanding Mode"], 1)
    } else {
        UI.SetEnabled(["Config", "[PASTED]Freestanding", "[PASTED]Freestanding", "Freestanding Mode"], 0)
    }
}

//UI可见性----------------------------------------------------------------------


//menu 设定结束---------------------------------------------------------------------------

//全局变量                              
var real = -60; //start var
var up = true
var LBY = -60;
var down = true
var fakelag = false;
var Trigger_fakelag = false;
var Fakelag_jitter = false;
var Loop_1 = 1;
var Loop_2 = 1;
var Loop_3 = 1;
var Shot = 0;
var BreakLeg = true

function LBYsway() {
    if (UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "AA mode"]) == 1) {
        var speed2 = (UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "LBY Sway Speed"]))
        var AngleC = (UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "LBY Sway Angle A"]))
        var AngleD = (UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "LBY Sway Angle B"]))
        AngleD = 0 - AngleD;
        if (down === true) {
            if (LBY <= AngleC && down == true) {
                LBY = LBY + speed2;
            }
            if (LBY >= AngleC) {
                down = false;
            }
        }
        if (down == false) {
            if (LBY >= -AngleD && down == false) {
                LBY = LBY - speed2;
            }
            if (LBY <= -AngleD) {
                down = true;
            }
        }
    }
}

function realsway() {
    if (UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "AA mode"]) == 1) {
        var speed = (UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "Real Sway Speed"]))
        var AngleA = (UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "Real Sway Angle A"]))
        var AngleB = (UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "Real Sway Angle B"]))
        AngleB = 0 - AngleB;
        if (up === true) {
            if (real <= AngleA && up == true) {
                real = real + speed;
            }
            if (real >= AngleA) {
                up = false;
            }
        }
        if (up == false) {
            if (real >= -AngleB && up == false) {
                real = real - speed;
            }
            if (real <= -AngleB) {
                up = true;
            }
        }
    }
}

var speed = false;

function Options() {
    if (UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "Yaw & jitter"]) && Entity.IsAlive(Entity.GetLocalPlayer())) {
        var MaxYaw = UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "Yaw & Jitter"])
        var MinYaw = 0 - UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "Yaw & Jitter"])
        var RandomYawJitter = UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "Random Yaw & Jitter"]);
        var yaw = Math.floor(Math.random() * (MaxYaw - MinYaw) + MinYaw);
        var speed_1 = 6;
        var speed_2 = UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "Random jitter speed"]);
        //JITTER 开始          
        if (RandomYawJitter == 1) {
            if (speed = false) {
                if (speed_1 > speed_2) {
                    UI.SetValue(["Rage", "Anti Aim", "Directions", "Jitter offset"], yaw);
                    speed_1 = 0
                }
                speed_1 = speed_1 + 1;
                speed = true;
            }

            if (speed = true) {
                if (speed_1 > speed_2) {
                    UI.SetValue(["Rage", "Anti Aim", "Directions", "Jitter offset"], yaw);
                    speed_1 = 0
                }
                speed_1 = speed_1 + 1;
                speed = false;
            }
        } else {
            UI.SetValue(["Rage", "Anti Aim", "Directions", "Jitter offset"], MaxYaw);
        }

        var MaxFake = UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "Fake Offset"])
        var MinFake = 0 - MaxFake;
        var offset = Math.random() * (MaxFake - MinFake) + MinFake;
        var RandomFakeOffset = UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "Random Fake Offset"])

        if (RandomFakeOffset == true) {
            AntiAim.SetFakeOffset(offset)
        } else {
            AntiAim.SetFakeOffset(MaxFake)
        }
    }

    if (UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "Fakelag & Anti-Brute"]) == 1 && UI.GetValue(["Config", "SUBTAB_MGR", "Scripts", "SHEET_MGR", "Keys", "JS Keybinds", "[FD]Keybind"]) == 0 && Entity.IsAlive(Entity.GetLocalPlayer())) {
        var max = UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "Fakelag Max"]);
        var min = UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "Fakelag Min"]);
        var trigger_max = UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "Trigger fakelag Max"]);
        var trigger_min = UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "Trigger fakelag Min"]);
        var FakeLagSpeed = UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "Fakelag Delay"])
        var trigger_fakeLagSpeed = UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "Trigger fakelag Delay"])
        var Jitter_fakeLagSpeed = UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "Fakelag jitter Delay"])
        var FinalLag = Math.floor(Math.random() * (max + 1 - min) + min);
        var Trigger_FinalLag = Math.floor(Math.random() * (trigger_max + 1 - trigger_min) + trigger_min);
        var Jittter_max = UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "Fakelag jitter Max"]);
        var Jittter_min = UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "Fakelag jitter Min"]);
        var Jitter_FinalLag = Math.floor(Math.random() * (Jittter_max + 1 - Jittter_min) + Jittter_min);

        if (fakelag = false) {
            if (Loop_1 > FakeLagSpeed) {
                UI.SetValue(["Rage", "Fake Lag", "Limit"], FinalLag);
                Loop_1 = 0
            }
            Loop_1 = Loop_1 + 1;
            Fakelag = true;
        }

        if (fakelag = true) {
            if (Loop_1 > FakeLagSpeed) {
                UI.SetValue(["Rage", "Fake Lag", "Limit"], FinalLag);
                Loop_1 = 0
            }
            Loop_1 = Loop_1 + 1;
            Fakelag = false;
        }

        if (Trigger_fakelag = false) {
            if (Loop_2 > trigger_fakeLagSpeed) {
                UI.SetValue(["Rage", "Fake Lag", "Trigger limit"], Trigger_FinalLag);
                Loop_2 = 0
            }
            Loop_2 = Loop_2 + 1;
            Trigger_fakelag = true;
        }

        if (Trigger_fakelag = true) {
            if (Loop_2 > trigger_fakeLagSpeed) {
                UI.SetValue(["Rage", "Fake Lag", "Trigger limit"], Trigger_FinalLag);
                Loop_2 = 0
            }
            Loop_2 = Loop_2 + 1;
            Trigger_fakelag = false;
        }

        if (Fakelag_jitter = false) {
            if (Loop_3 > Jitter_fakeLagSpeed) {
                UI.SetValue(["Rage", "Fake Lag", "Jitter"], Jitter_FinalLag);
                Loop_3 = 0
            }
            Loop_3 = Loop_3 + 1;
            Fakelag_jitter = true;
        }

        if (Fakelag_jitter = true) {
            if (Loop_3 > Jitter_fakeLagSpeed) {
                UI.SetValue(["Rage", "Fake Lag", "Jitter"], Jitter_FinalLag);
                Loop_3 = 0
            }
            Loop_3 = Loop_3 + 1;
            Fakelag_jitter = false;
        }
    } else {
//none
    }
}

//--> sway AA invert

function antiaim() {
    if (UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "AA mode"]) == 1) {
        if (UI.GetValue(["Rage", "Anti Aim", "General", "Key assignment", "AA Direction inverter"]) == 1) {
            AntiAim.SetOverride(1)
            AntiAim.SetRealOffset(real)
            AntiAim.SetLBYOffset(LBY)
        } else {
            AntiAim.SetOverride(1)
            AntiAim.SetRealOffset(0 - real)
            AntiAim.SetLBYOffset(0 - LBY)
        }
    }
}

//--> sway AA invert

//BreakLag 

function AnimationBreak() {
    UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "Fakelag & Anti-Brute"]) && UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "Break leg"]) && (trufalse = 10 * Math.abs(Math.sin(64 * Globals.Realtime())), trufalse > 5 &&
        UI.SetValue(["Misc.", "Movement", "Leg movement"], 0), trufalse < 8 && UI.SetValue(["Misc.", "Movement", "Leg movement"], 1))
}
//BreakLag 



//返回速度-----------------------------------------

function getVelocity(index) {
    var velocity = Entity.GetProp(index, 'CBasePlayer', 'm_vecVelocity[0]');
    return Math.sqrt(velocity[0] * velocity[0] + velocity[1] * velocity[1]);
}

//返回速度-----------------------------------------




//Fakelag 逻辑函数-------------------------------------------------------

function clantag() {
    if (UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "Fakelag & Anti-Brute"])) {
        var velocity = getVelocity(Entity.GetLocalPlayer())
        if (UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "FakeLag On Move"]) == 1) {
            if (velocity > 90) {
                UI.SetValue(["Rage", "Fake Lag", "General", "Limit"], UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "Move Fakelag"]));
            }
        }
        if (UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "Fakelag On Auto Stop"]) == 1) {
            if (velocity < 60) {
                UI.SetValue(["Rage", "Fake Lag", "General", "Limit"], UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "Auto Stop Fakelag"]));
            }
        }
    }
}

//Fakelag 逻辑函数-------------------------------------------------------




//Anti Bruteforce 函数-----------------------------------------------------
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

//Anti Bruteforce 函数----------------------------------------------------




//on shot 逻辑函数-------------------------------------------------------

var other_weapons = [
    "knife",
    "knife_t",
    "hegrenade",
    "smokegrenade",
    "molotov",
    "incgrenade",
    "flashbang",
    "decoy",
    "taser"
];

function is_gun(weapon_name) {
    for (var i = 0; i < other_weapons.length; i++) {
        if (weapon_name == "weapon_" + other_weapons[i]) {
            return false;
        }
    }
    return true;
}

var shot;

function shoting() {
    player_id = Event.GetInt("userid");
    player_weapon = Event.GetString("weapon");
    onshot = Entity.IsLocalPlayer(Entity.GetEntityFromUserID(player_id)) && is_gun(player_weapon)
    shot_FL = UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "On shot fakelag"])
    if (UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "On shot mode"])) {
        if (onshot) {
            shot = true
        }
    }
}

function shotFL() {
    shot_FL = UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "On shot fakelag"])
    var is_valve_server = Entity.GetProp(Entity.GetGameRulesProxy(), "CCSGameRulesProxy", "m_bIsValveDS");
    if (areExploits()) {
        UserCMD.Send()
    }
    if (UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "On shot mode"]) && !is_valve_server) {
        if (shot && shot_FL > 6 && !areExploits()) {
            UI.SetValue(["Rage", "Fake Lag", "General", "Limit"], 16);
            AntiAim.SetOverride(0);
            UserCMD.Choke()
            shot = false
        }

        if (shot && shot_FL < 7 && !areExploits()) {
            UI.SetValue(["Rage", "Fake Lag", "General", "Limit"], 0);
            AntiAim.SetOverride(0);
            UserCMD.Send()
            shot = false
        }

        if (shot && areExploits()) {
            UI.SetValue(["Rage", "Fake Lag", "General", "Limit"], 0);
            AntiAim.SetOverride(0);
            UserCMD.Send()
            shot = false
        }
    }
    if (UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "On shot mode"]) && is_valve_server) {
        if (shot && shot_FL > 6 && !areExploits()) {
            UI.SetValue(["Rage", "Fake Lag", "General", "Limit"], 6);
            AntiAim.SetOverride(0);
            UserCMD.Choke()
            shot = false
        }

        if (shot && shot_FL < 7 && !areExploits()) {
            UI.SetValue(["Rage", "Fake Lag", "General", "Limit"], 0);
            AntiAim.SetOverride(0);
            UserCMD.Send();
            shot = false
        }

        if (shot && areExploits()) {
            UI.SetValue(["Rage", "Fake Lag", "General", "Limit"], 0);
            AntiAim.SetOverride(0);
            UserCMD.Send();
            shot = false
        }
    }

    if (UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "Dynamic desync on shot"])) {
        trufalse = 67 * Math.abs(Math.sin(64 * Globals.Realtime())), trufalse > 20 && UI.SetValue(["Rage", "Anti Aim", "SHEET_MGR", "On-shot desync"], 0), trufalse < 20 && UI.SetValue(["Rage", "Anti Aim", "SHEET_MGR", "On-shot desync"], 1)
    }
}

//on shot 逻辑函数-------------------------------------------------------




//custom AA 主函数-----------------------------------------------------------

function LimFake() {
    var LBYDelta = UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "LBY Delta"]);
    var RealDelta = UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "Real Delta"]);
    var InvertedLBYDelta = UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "Inverted LBY Delta"]);
    var InvertedRealDelta = UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "Inverted Real Delta"]);

    //--------------------------------------------------------------------------------------//
    if (UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "AA mode"]) == 2) {
        if (UI.GetValue(["Rage", "Anti Aim", "General", "Key assignment", "AA Direction inverter"]) == 1) {
            AntiAim.SetOverride(1);
            AntiAim.SetRealOffset(InvertedRealDelta);
            AntiAim.SetLBYOffset(InvertedLBYDelta);
        } else {
            AntiAim.SetOverride(1);
            AntiAim.SetRealOffset(RealDelta);
            AntiAim.SetLBYOffset(LBYDelta);
        }
    }
}

//custom AA 主函数-----------------------------------------------------------


//testing!!!!!!!!! freestanding 函数段---------------------------------------------------

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

//testing!!!!!!!!! freestanding 函数段---------------------------------------------------



//Advanced sway AA

//全局变量----------------------------------------
var timer = false;
var down = false;
var man_timer = false;
lll = false;
a = 0;
var czz = 0;
var slide = false;
var fakeoff = 1;
var slideYonsn = 0;
man_init = false;
yawYonsn = 0;
rgb_r = 0;
rgb_g = 100;
rgb_b = 255;
current_preset = 0;
var sw_timer = false;
var sw_cur = 1;
exploit_on = false;
var lastTime = 0;
var hittime = 0;
var FREESTAND = false;
//全局变量----------------------------------------



function Freestanding() {
    if (UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "AA mode"]) == 3) {
        if (!UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "Freestand On Hit"]))
            return;

        FREESTAND = 0;

        if ((hittime + UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "Freestand Duration"]) > Global.Curtime()))
            FREESTAND = 1;

        UI.SetValue(["Rage", "Anti Aim", "Directions", "Auto direction"], FREESTAND);
    }
}

var jitter_cache = UI.GetValue(["Rage", "Anti Aim", "Directions", "Jitter offset"])
var yaw_cache = UI.GetValue(["Rage", "Anti Aim", "Directions", "Yaw offset"])

//walkAA 逻辑段-----------------------------------------------------------------------------

function Walk_AA() {
    if (UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "AA mode"]) == 3) {
        localplayer_index = Entity.GetLocalPlayer();


        if (UI.GetValue(["Rage", "Anti Aim", "General", "Key assignment", "Tank Walk"])) {
            UI.SetValue(["Rage", "Anti Aim", "Directions", "Yaw offset"], 2);
            UI.SetValue(["Rage", "Anti Aim", "Directions", "Jitter offset"], -2);
            AntiAim.SetOverride(1);
            AntiAim.SetFakeOffset(-2);
            AntiAim.SetRealOffset(-32);

        }
    }
}


function getVal(valName) { return UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", valName]); }

function cMove() {
    if (UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "AA mode"]) == 3) {
        //forward, side, up.
        if (!UI.GetValue(["Rage", "Anti Aim", "General", "Key assignment", "Tank Walk"])) return;

        speed = getVal("Speed:");

        fSpeed = speed;
        bSpeed = speed;
        sSpeed = speed;


        dir = [0, 0, 0];

        if (Input.IsKeyPressed(0x57)) {
            //'W' AKA Forward
            dir[0] += fSpeed;
        }
        if (Input.IsKeyPressed(0x44)) {
            //'D' AKA Right
            dir[1] += sSpeed;
        }
        if (Input.IsKeyPressed(0x41)) {
            //'A' AKA Left
            dir[1] -= sSpeed;
        }
        if (Input.IsKeyPressed(0x53)) {
            //'S' AKA Back
            dir[0] -= bSpeed;
        }

        UserCMD.SetMovement(dir);
    }
}

function ClosestPointOnRay(target, rayStart, rayEnd) {
    var to = VectorSubtract(target, rayStart);
    var dir = VectorSubtract(rayEnd, rayStart);
    var length = VectorLength(dir[0], dir[1], dir[2]);
    dir = VectorNormalize(dir);


    function GetScriptOption(name) {
        var Value = UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", name]);
        return Value;
    }


    var rangeAlong = VectorDot(dir, to);
    if (rangeAlong < 0.0) {
        return rayStart;
    }
    if (rangeAlong > length) {
        return rayEnd;
    }
    return VectorAdd(rayStart, VectorMultiply(dir, [rangeAlong, rangeAlong, rangeAlong]));
}
//walkAA 逻辑段-----------------------------------------------------------------------------


//-----------------------------------------------------------------------------------------------
var lastHitTime = 0.0;
var lastImpactTimes =
    [
        0.0
    ];
var lastImpacts =
    [
        [0.0, 0.0, 0.0]
    ];
//-----------------------------------------------------------------------------------------------


//AA 主函数---------------------------------------------------------------------------------------

function antiaimloop() {
    if (UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "AA mode"]) == 3) {
        AntiAim.SetOverride(1);
        var $typeface = UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "Advanced Jitter"]);
        var $off = UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "Offset Break"]);
        var $sway = UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "AA-Swing"]);
        var $switch = UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "AntiAim-Switch"]);
        var $fake = getScriptVal("False jitter");
        if (getScriptVal("Presets") !== current_preset) {
            loadPreset(getScriptVal("Presets"));
            current_preset = getScriptVal("Presets");
        }
        if (!$typeface) {
            UI.SetValue(["Rage", "Anti Aim", "Directions", "Jitter offset"], 0);
        }
        if ($typeface) {
            var $Range = UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "Jitter limit"]);
            var bg = $Range;
            var sg = ($Range * -1);
            min = Math.ceil(sg);
            max = Math.floor(bg);
            AntiAim.SetOverride(1);
            var subVal = (Math.floor(Math.random(subVal) * (max - min)) + min);
            var rem = subVal / 2;
            UI.SetValue(["Rage", "Anti Aim", "Directions", "Yaw offset"], rem);
            UI.SetValue(["Rage", "Anti Aim", "Directions", "Jitter offset"], subVal);
        }
        if ($off) {
            var m2 = m2 + m1;
            var m1 = Math.floor(Math.random() * 100) - 50;
            var c1 = Math.floor((Math.random() * 50)) - 25;
            var offsetVal = (m1 * -1);
            AntiAim.SetOverride(1);
            AntiAim.SetFakeOffset(m1);
            AntiAim.SetRealOffset(offsetVal);
        }
        {
            isInverted = UI.GetValue(["Rage", "Anti Aim", "General", "Key assignment", 'AA Direction inverter']);
            slideRange = UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "Sway Range"]);
            slideRate = UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "Sway frequency"]);
            limit = UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "Swing astrict"]);
            LimitYonsn = UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "Sway Amount"]);
            var fake = Math.floor(Math.random() * (25 - 2) + 2);
            if (!limit) {
                if (slide) {
                    if (slideYonsn > (slideRange / 2)) {
                        slide = false;
                    } else {
                        slideYonsn += slideRate;
                    }
                } else {
                    if (slideYonsn < -(slideRange / 2)) {
                        slide = true;
                    } else {
                        slideYonsn -= slideRate;
                    }
                }
                slideRange += slideYonsn;
            } else if (limit) {
                if (slide) {
                    if (slideYonsn > slideRange / 2) {
                        slide = false;
                    } else {
                        slideYonsn += slideRate;
                    }
                } else {
                    if (slideYonsn < LimitYonsn / 2) {
                        slide = true;
                    } else {
                        slideYonsn -= slideRate;
                    }
                }
            }
var left = -slideYonsn + fake / fake * 0.6
var right = slideYonsn - fake / fake * 0.8

            if ($sway && !isInverted) {
                AntiAim.SetOverride(1);
                AntiAim.SetFakeOffset(0);
                AntiAim.SetRealOffset(slideYonsn - fake * 0.20);
               AntiAim.SetLBYOffset(left);
            } else if ($sway && isInverted) {
                AntiAim.SetOverride(1);
                AntiAim.SetFakeOffset(0);
                AntiAim.SetRealOffset(-slideYonsn - fake * 0.20);
               AntiAim.SetLBYOffset(right);
            }
        }
        if ($fake) {
            FJ_Step = UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "False jitter Step"]);
            FJ_Range = UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "False jitter Range"]);
            FJ_Speed = UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "False jitter Speed"]);
            FJ_Extend = ((1e-9) / (FJ_Speed * 0x4ee0d1d72fd4780000000000000));
            FJ_Retract = 1e-22 / (FJ_Speed * 0x7e3482f1e620c0000000000000);
            AntiAim.SetOverride(1);
            if ((a < FJ_Range) && !down) {
                if (!timer) {
                    lasttime = Globals.Curtime();
                    timer = true;
                }
                if (Globals.Curtime() >= (lasttime + FJ_Extend)) {
                    a += FJ_Step;
                    if (!areExploits()) {
                        AntiAim.SetFakeOffset(0);
                        if (!isInverted) {
                            AntiAim.SetLBYOffset(a);
                        } else if (isInverted) {
                            AntiAim.SetLBYOffset(-a);
                        }
                    } else {
                        if (!isInverted) {
                            AntiAim.SetFakeOffset(a);
                            AntiAim.SetFakeOffset(-a);
                        } else if (isInverted) {
                            AntiAim.SetFakeOffset(-a);
                            AntiAim.SetFakeOffset(a);
                        }
                    }
                    timer = false;
                }
            } else if ((a >= FJ_Range) || down) {
                down = true;
                if (a <= 0) {
                    down = false;
                }
                if (!timer) {
                    lasttime = Globals.Curtime();
                    timer = true;
                }
                if (Globals.Curtime() >= (lasttime + FJ_Retract)) {
                    a -= FJ_Step;
                    if (!areExploits()) {
                        AntiAim.SetFakeOffset(0);
                        if (!isInverted) {
                            AntiAim.SetLBYOffset(a);
                        } else if (isInverted) {
                            AntiAim.SetLBYOffset(-a);
                        }
                    } else {
                        if (!isInverted) {
                            AntiAim.SetFakeOffset(a);
                            AntiAim.SetFakeOffset(-a);
                        } else if (isInverted) {
                            AntiAim.SetFakeOffset(-a);
                            AntiAim.SetFakeOffset(a);
                        }
                    }
                    timer = false;
                }
            }
        }

        //AA 主函数---------------------------------------------------------------------------------------





        //yaw 切换 ---------------------------------------------------------------------------------

        if ($switch) {
            switchC1 = UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "Switch Yaw - A"]);
            switchC2 = UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "Switch Yaw - B"]);
            switchC3 = UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "Switch Yaw - C"]);
            switchDelay = UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++", "Switch Delay"]);
            sw_delay = 0.001 * switchDelay;
            if (!sw_timer) {
                sw_lasttime = Globals.Curtime();
                sw_timer = true;
            }
            if (Globals.Curtime() >= sw_lasttime + sw_delay) {
                if (sw_cur == 1) {
                    sw_val = switchC2;
                    sw_cur += 1;
                    sw_timer = false;
                } else if (sw_cur == 2) {
                    sw_val = switchC3;
                    sw_cur += 1;
                    sw_timer = false;
                } else if (sw_cur == 3) {
                    sw_val = switchC1;
                    sw_cur = 1;
                    sw_timer = false;
                }
                if (!isInverted) {
                    UI.SetValue(["Rage", "Anti Aim", "Directions", "Yaw offset"], sw_val);
                } else if (isInverted) {
                    UI.SetValue(["Rage", "Anti Aim", "Directions", "Yaw offset"], -sw_val);
                }
            }
        }
    }
}
//yaw 切换 ---------------------------------------------------------------------------------

function onFire() {
    return;
}

//逻辑段------------------------------------------------------------------------

function setYaw(yaw) {
    UI.SetValue(["Rage", "Anti Aim", "Directions", "Yaw offset", yaw]);
}

function rand_int(min, max) {
    return Math.floor(Math.random() * ((max - min) + 1) + min);
}


function getScriptVal(name) {
    return UI.GetValue(["Config", "Anti-Aim++", "Anti-Aim++"], name);
}
/*
function setScriptVal(key, value) {
    UI.SetValue(["Config", "Anti-Aim++", "Anti-Aim++", key], value);
}
*/

function areExploits() {

    if (UI.GetValue(["Rage", "Exploits", "Keys", "Double tap"]) || UI.GetValue(["Rage", "Exploits", "Keys", "Hide shots"])) {
        if (!exploit_on) {
            OG_FJspeed = getScriptVal("False jitter Speed");
            OG_FJrange = getScriptVal("False jitter Range");
            OG_FJstep = getScriptVal("False jitter Step");
        }
        UI.SetValue(["Config", "Anti-Aim++", "Anti-Aim++","False jitter Speed"], 90);
        UI.SetValue(["Config", "Anti-Aim++", "Anti-Aim++","False jitter Range"], 11);
        UI.SetValue(["Config", "Anti-Aim++", "Anti-Aim++","False jitter Step"], 8);
        exploit_on = true;
        return true;
    } else {
        if (exploit_on) {
//            UI.SetValue(["Config", "Anti-Aim++", "Anti-Aim++","False jitter Speed"], OG_FJspeed);
  //          UI.SetValue(["Config", "Anti-Aim++", "Anti-Aim++","False jitter Range"], OG_FJrange);
   //         UI.SetValue(["Config", "Anti-Aim++", "Anti-Aim++","False jitter Step"], OG_FJstep);
        }
        exploit_on = false;
        return false;
    }
}

function loadPreset(parms) {
    switch (parms) {
        case 0:
            return;
            break;
        case 1:
            p_isAdvancedJitter = 1;
            p_AdvancedRange = -5;
            p_isOffsetBreak = 0;
            p_isSway = 1;
            p_isSwayLimit = 1;
            p_LimitRange = 17;
            p_swayRange = 45;
            p_swaySpeed = 2;
            p_isFakeJitter = 1;
            p_FJspeed = 15;
            p_FJrange = 15;
            p_FJstep = 3;
            p_isSwitchAA = 1;
            p_yawVal1 = -3;
            p_yawVal2 = -2;
            p_yawVal3 = -1;
            break;
        case 2:
            p_isAdvancedJitter = 1;
            p_AdvancedRange = -14;
            p_isOffsetBreak = 1;
            p_isSway = 1;
            p_isSwayLimit = 0;
            p_LimitRange = 34;
            p_swayRange = 87;
            p_swaySpeed = 14;
            p_isFakeJitter = 1;
            p_FJspeed = 25;
            p_FJrange = 34;
            p_FJstep = 6;
            p_isSwitchAA = 1;
            p_yawVal1 = -1;
            p_yawVal2 = -5;
            p_yawVal3 = -2;
            break;
        case 3:
            p_isAdvancedJitter = 0;
            p_AdvancedRange = 0;
            p_isOffsetBreak = 0;
            p_isSway = 0;
            p_isSwayLimit = 0;
            p_LimitRange = 0;
            p_swayRange = 0;
            p_swaySpeed = 0;
            p_isFakeJitter = 0;
            p_FJspeed = 0;
            p_FJrange = 0;
            p_FJstep = 0;
            p_isSwitchAA = 0;
            p_yawVal1 = 0;
            p_yawVal2 = -10;
            p_yawVal3 = 0;
            break;
        default:
            return;
            break;
    }
    UI.SetValue(["Config", "Anti-Aim++", "Anti-Aim++","Advanced Jitter"], p_isAdvancedJitter);
    UI.SetValue(["Config", "Anti-Aim++", "Anti-Aim++","Range"], p_AdvancedRange);
    UI.SetValue(["Config", "Anti-Aim++", "Anti-Aim++","Offset Break"], p_isOffsetBreak);
    UI.SetValue(["Config", "Anti-Aim++", "Anti-Aim++","AA-Swing"], p_isSway);
    UI.SetValue(["Config", "Anti-Aim++", "Anti-Aim++","Swing astrict"], p_isSwayLimit);
    UI.SetValue(["Config", "Anti-Aim++", "Anti-Aim++","Sway Amount"], p_LimitRange);
    UI.SetValue(["Config", "Anti-Aim++", "Anti-Aim++","Sway Range"], p_swayRange);
    UI.SetValue(["Config", "Anti-Aim++", "Anti-Aim++","Sway frequency"], p_swaySpeed);
    UI.SetValue(["Config", "Anti-Aim++", "Anti-Aim++","False jitter"], p_isFakeJitter);
    UI.SetValue(["Config", "Anti-Aim++", "Anti-Aim++","False jitter Speed"], p_FJspeed);
    UI.SetValue(["Config", "Anti-Aim++", "Anti-Aim++","False jitter Range"], p_FJrange);
    UI.SetValue(["Config", "Anti-Aim++", "Anti-Aim++","False jitter Step"], p_FJstep);
    UI.SetValue(["Config", "Anti-Aim++", "Anti-Aim++","AntiAim-Switch"], p_isSwitchAA);
    UI.SetValue(["Config", "Anti-Aim++", "Anti-Aim++","Switch Yaw - A"], p_yawVal1);
    UI.SetValue(["Config", "Anti-Aim++", "Anti-Aim++","Switch Yaw - B"], p_yawVal1);
    UI.SetValue(["Config", "Anti-Aim++", "Anti-Aim++","Switch Yaw - C"], p_yawVal1);
}

//逻辑段------------------------------------------------------------------------


//--> Misc. --> skin changer helper

var old_index = -1;

const weapons = {
    1: 5,
    2: 6,
    3: 8,
    4: 11,
    7: 0,
    8: 1,
    9: 2,
    10: 7,
    11: 9,
    13: 10,
    14: 13,
    16: 14,
    17: 16,
    19: 24,
    23: 19,
    24: 31,
    25: 33,
    26: 3,
    27: 17,
    28: 21,
    29: 26,
    30: 30,
    32: 12,
    33: 18,
    34: 20,
    35: 22,
    36: 23,
    38: 38,
    39: 28,
    40: 29,
    60: 15,
    61: 32,
    63: 4,
    64: 25,
    500: 34,
    503: 48,
    505: 35,
    506: 36,
    507: 37,
    508: 38,
    509: 45,
    512: 40,
    514: 44,
    515: 39,
    516: 42,
    519: 47,
    520: 41,
    522: 43,
    523: 46,
    517: 49,
    518: 50,
    521: 51,
    525: 52
}


function schanger() {

    const player = Entity.GetLocalPlayer();

    const wpn_index = Entity.GetProp(Entity.GetWeapon(player), "CBaseAttributableItem", "m_iItemDefinitionIndex") & 0xFFFF;

    if (wpn_index === old_index) {
        return;
    }

    old_index = wpn_index;

    if (wpn_index in weapons) {

        const menu = wpn_index

        UI.SetValue(["Misc.", "Skins", "Skins", "Weapon"], menu);
    }
}

//--> Misc. --> skin changer helper


//--> Misc. --> Fix skybox

var wasmadetransparent = false;

function ensure_requirements_met(){
    UI.SetValue(["Misc.", "Helpers", "SHEET_MGR", "Client", "Bypass sv_pure"], 1);
    UI.SetValue(["Misc.", "Helpers", "SHEET_MGR", "Client", "Force sv_cheats"], 1);
}

function get_skybox(){
 if (UI.GetString(["Visuals", "World", "SHEET_MGR", "General", "Skybox"]) == "Custom")
    return UI.GetString(["Visuals", "World", "SHEET_MGR", "General", "Custom skybox"]);
 else
    return UI.GetString(["Visuals", "World", "SHEET_MGR", "General", "Skybox"]);
}

function maketransparent(){
    Cheat.ExecuteCommand ("mat_suppress \"models/props/de_nuke/hr_nuke/nuke_skydome_001/nuke_clouds_001\"");
        Cheat.ExecuteCommand ("mat_suppress \"models/props/de_nuke/hr_nuke/nuke_skydome_001/nuke_clouds_002\"");
        Cheat.ExecuteCommand ("mat_suppress \"models\props\de_cbble\dist_mountain_a\dist_mountain_a.mdl\"");
    Cheat.ExecuteCommand ("mat_suppress \"models/props/de_nuke/hr_nuke/nuke_skydome_001/nuke_skydome_001\"");
    Cheat.ExecuteCommand ("mat_suppress \"models/props/de_dust/hr_dust/dust_skybox/sky_dust2\"");
    wasmadetransparent = true;
}

function fix_skybox() {
    var map = World.GetMapName();
    ensure_requirements_met()

    if (map == "de_inferno" || map == "de_nuke" || map == "de_dust2" || map == "de_train" || map == "de_cbble")
    {
    if (wasmadetransparent == false)
        maketransparent();

    Convar.SetString("sv_skyname", get_skybox());
    }
}

function init(){
  if (World.GetServerString() != '')
    fix_skybox();   
}
init();

function reset_trasnparent(){
    wasmadetransparent = false;
}

//--> Misc. --> Fix skybox

function onUnload() {
    AntiAim.SetOverride(0);
    Convar.SetInt("cl_hud_color", clhc);
    Local.SetClanTag("");
    Convar.SetFloat("r_aspectratio", orgaspect);
    Exploit.EnableRecharge()
    UI.SetValue(["Cheat", "SHEET_MGR", "General", "Restrictions"], 1);
    UI.SetEnabled(["Config", "Cheat", "General", "RAGE QUIT"], 0)
    Exploit.EnableRecharge();
    UI.SetValue(["Misc.", "Helpers", "Client", "Force sv_cheats"], 1);
    Convar.SetFloat("sv_airaccelerate", 12);
    UI.SetValue(ref_turnspeed, cache.turn_speed);
}

//sway AA 运行
function Functions() {
    autowall();
    antiaim();
    realsway();
    LBYsway();
    Options();
    clantag();
}

//Menu 函数库

function HSVtoRGB(h, s, v) {
    var r, g, b, i, f, p, q, t;

    i = Math.floor(h * 6);
    f = h * 6 - i;
    p = v * (1 - s);
    q = v * (1 - f * s);
    t = v * (1 - (1 - f) * s);

    switch (i % 6) {
        case 0:
            r = v, g = t, b = p;
            break;
        case 1:
            r = q, g = v, b = p;
            break;
        case 2:
            r = p, g = v, b = t;
            break;
        case 3:
            r = p, g = q, b = v;
            break;
        case 4:
            r = t, g = p, b = v;
            break;
        case 5:
            r = v, g = p, b = q;
            break;
    }
    return {
        r: Math.round(r * 255),
        g: Math.round(g * 255),
        b: Math.round(b * 255)
    };
}

function RGB(h, s, v) {
    var r, g, b, i, f, p, q, t;
    if (arguments.length === 1) {
        s = h.s, v = h.v, h = h.h;
    }
    i = Math.floor(h * 6);
    f = h * 6 - i;
    p = v * (1 - s);
    q = v * (1 - f * s);
    t = v * (1 - (1 - f) * s);
    switch (i % 6) {
        case 0:
            r = v, g = t, b = p;
            break;
        case 1:
            r = q, g = v, b = p;
            break;
        case 2:
            r = p, g = v, b = t;
            break;
        case 3:
            r = p, g = q, b = v;
            break;
        case 4:
            r = t, g = p, b = v;
            break;
        case 5:
            r = v, g = p, b = q;
            break;
    }
    return {
        r: Math.round(r * 255),
        g: Math.round(g * 255),
        b: Math.round(b * 255)
    };
}

function HSV2RGB(h, s, v) {
    var r, g, b, i, f, p, q, t;

    i = Math.floor(h * 6);
    f = h * 6 - i;
    p = v * (1 - s);
    q = v * (1 - f * s);
    t = v * (1 - (1 - f) * s);

    switch (i % 6) {
        case 0:
            r = v,
                g = t,
                b = p;
            break;
        case 1:
            r = q,
                g = v,
                b = p;
            break;
        case 2:
            r = p,
                g = v,
                b = t;
            break;
        case 3:
            r = p,
                g = q,
                b = v;
            break;
        case 4:
            r = t,
                g = p,
                b = v;
            break;
        case 5:
            r = v,
                g = p,
                b = q;
            break;
    }

    return {
        r: Math.round(r * 255),
        g: Math.round(g * 255),
        b: Math.round(b * 255)
    };
}

function draw_circle_3d(x, y, z, radius, degrees, start_at, clr, fill_clr) {
    var accuracy = 8;
    var old_x, old_y;
    degrees = degrees < 361 && degrees || 360;
    degrees = degrees > -1 && degrees || 0
    start_at = start_at + 1
    for (rot = start_at; rot < degrees + start_at + 1; rot += start_at * accuracy) {
        rot_r = rot * (Math.PI / 180)
        line_x = radius * Math.cos(rot_r) + x, line_y = radius * Math.sin(rot_r) + y
        var curr = Render.WorldToScreen([line_x, line_y, z]),
            cur = Render.WorldToScreen([x, y, z]);
        if (cur[0] != null && curr[0] != null && old_x != null) {
            Render.Polygon([
                [curr[0], curr[1]],
                [old_x, old_y],
                [cur[0], cur[1]]
            ], fill_clr)
            Render.Line(curr[0], curr[1], old_x, old_y, clr)
        }
        old_x = curr[0], old_y = curr[1];
    }
}

function normalize_yaw(angle) {
    var adjusted_yaw = angle;

    if (adjusted_yaw < -180)
        adjusted_yaw += 360;

    if (adjusted_yaw > 180)
        adjusted_yaw -= 360;

    return adjusted_yaw;
}

function draw_arc(x, y, radius, start_angle, percent, thickness, color) {
    var precision = (2 * Math.PI) / 30;
    var step = Math.PI / 180;
    var inner = radius - thickness;
    var end_angle = (start_angle + percent) * step;
    var start_angle = (start_angle * Math.PI) / 180;

    for (; radius > inner; --radius) {
        for (var angle = start_angle; angle < end_angle; angle += precision) {
            var cx = Math.round(x + radius * Math.cos(angle));
            var cy = Math.round(y + radius * Math.sin(angle));

            var cx2 = Math.round(x + radius * Math.cos(angle + precision));
            var cy2 = Math.round(y + radius * Math.sin(angle + precision));

            Render.Line(cx, cy, cx2, cy2, color);
        }
    }
}

function DEG2RAD(degree) {
    return (Math.PI / 180) * degree;
}

function ANGLE2VEC(angle) {
    pitch = angle[0];
    yaw = angle[1];
    return [Math.cos(DEG2RAD(pitch)) * Math.cos(DEG2RAD(yaw)), Math.cos(DEG2RAD(pitch)) * Math.sin(DEG2RAD(yaw)), -Math.sin(DEG2RAD(pitch))];
}

function getWallDistance(entity, angle) {
    vector = ANGLE2VEC(angle);
    origin = Entity.GetRenderOrigin(entity);
    origin[2] += Entity.GetProp(entity, "CBasePlayer", "m_vecViewOffset[2]")[0];
    end = [origin[0] + vector[0] * 8192, origin[1] + vector[1] * 8192, origin[2] + vector[2] * 8192];
    result = Trace.Line(entity, origin, end);
    if (result[1] != 1) {
        wall = [origin[0] + vector[0] * result[1] * 8192, origin[1] + vector[1] * result[1] * 8192, origin[2] + vector[2] * result[1] * 8192];
        distance = Math.sqrt(Math.pow(origin[0] - wall[0], 2) + Math.pow(origin[1] - wall[1], 2) + Math.pow(origin[2] - wall[2], 2));
        return distance;
    } else {
        return 0;
    }
}
//Weapon Config

//变量
//----------------------------------------------------------------------------\\
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
//----------------------------------------------------------------------------\\

function unload() {
    Exploit.EnableRecharge()
}

//----------------------------------------------------------------------------\\

//回调-------------------------------------------------------------------------

//Menu indicator
Cheat.RegisterCallback('Draw', 'Draw_invert');

//Welcome 回调
Cheat.RegisterCallback("player_connect_full", "initialize");

//hitmarker 回调
Cheat.RegisterCallback("Draw", "on_paint");
Cheat.RegisterCallback("player_hurt", "player_hurt");
Cheat.RegisterCallback("player_hurt", "player_damage_handler");

//jump shot 回调
Cheat.RegisterCallback('CreateMove', 'AirHitchance');

//Free camera 回调
Cheat.RegisterCallback("Draw", "Draw_freecamera");
Cheat.RegisterCallback("Draw", "showDelayedCamera")
Cheat.RegisterCallback("CreateMove", "calcDelayedCamera")

//Slowwalk assist 回调
Cheat.RegisterCallback("CreateMove", "cMove_1");

//watermark 回调
Cheat.RegisterCallback("Draw", "draw_");

//Hiteffect 回调
Global.RegisterCallback("player_hurt", "on_death");
Global.RegisterCallback("Draw", "render_effect");

//pitch set 回调
Cheat.RegisterCallback("Draw", "pitchZeroOnLand");

//Bullet Tracer 回调
Cheat.RegisterCallback("Draw", "draw_local");
Cheat.RegisterCallback('bullet_impact', 'UI_onBulletImpact');

//Grandes radius 回调
Cheat.RegisterCallback("round_start", "clearData");
Cheat.RegisterCallback("smokegrenade_detonate", "smokeStart");
Cheat.RegisterCallback("smokegrenade_expired", "smokeExpire");
Cheat.RegisterCallback("Draw", "onDraw");

//Log in chat 回调
Global.RegisterCallback("vote_options", "onVoteOptions");
Global.RegisterCallback("vote_cast", "onVoteCast");
Global.RegisterCallback("item_purchase", "BuyLogs");
Cheat.RegisterCallback("ragebot_fire", "ragebot_fire_1");
Cheat.RegisterCallback("player_hurt", "hurt");

//Filp swich weapon 回调
Global.RegisterCallback("weapon_fire", "on_weapon_fire");
Global.RegisterCallback("CreateMove", "reset_tick");

//trigger autowall 回调
Cheat.RegisterCallback("CreateMove", "autowall")

//dt伤害预测
Cheat.RegisterCallback("CreateMove", "mindmg")

//dt充值回调
Cheat.RegisterCallback("CreateMove", "_TBC_CREATE_MOVE");

//misc 回调
Cheat.RegisterCallback("Draw", "Ct");
Cheat.RegisterCallback("FrameStageNotify", "aspect");
Cheat.RegisterCallback("Draw", "rainbow");

//mm fake duck (官配假蹲) 回调
Cheat.RegisterCallback("ragebot_fire", 'ragebot_fire');
Cheat.RegisterCallback("Draw", "indicator");
Cheat.RegisterCallback("CreateMove", "auth_ok")
Cheat.RegisterCallback("CreateMove", "fastDuckUpdate");

//UI 显示/隐藏 回调
Cheat.RegisterCallback("Draw", "UIEnabled");

//AA 回调
Cheat.RegisterCallback("CreateMove", "Options")
Cheat.RegisterCallback("Draw", "Functions");

//Break leg 回调
Cheat.RegisterCallback("CreateMove", "AnimationBreak")

//anti burte force 回调
Cheat.RegisterCallback("player_hurt", "OnHurt");
Cheat.RegisterCallback("bullet_impact", "OnBulletImpact");

//on shot 逻辑回调
Cheat.RegisterCallback("weapon_fire", "shoting");
Cheat.RegisterCallback("CreateMove", "shotFL");

//mode 2 AA : "custom AA" 回调
Cheat.RegisterCallback("CreateMove", "LimFake");

//freestanding 回调
Cheat.RegisterCallback("CreateMove", "Freestanding_")

//mode 3 AA : Advanced sway AA回调
Cheat.RegisterCallback("CreateMove", "antiaimloop");
Cheat.RegisterCallback("CreateMove", "Walk_AA");
Cheat.RegisterCallback("CreateMove", "cMove");
Cheat.RegisterCallback("player_hurt", "OnHurt");
Cheat.RegisterCallback("Draw", "Freestanding");

//Weapon config 回调
Cheat.RegisterCallback("Unload", "unload");
Cheat.RegisterCallback("Draw", "onMenuUpdate");
Cheat.RegisterCallback("CreateMove", "Weapon_onCreateMove");
Cheat.RegisterCallback("weapon_fire", "onWeaponFire");

//--> Misc.
Cheat.RegisterCallback("CreateMove", "schanger")
Cheat.RegisterCallback("round_start", "fix_skybox")
Cheat.RegisterCallback("player_connect_full", "reset_trasnparent")
Cheat.RegisterCallback("Draw", "comicSans");
Cheat.RegisterCallback("Unload", "onUnload");

//回调-------------------------------------------------------------
```

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
