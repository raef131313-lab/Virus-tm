

import os
import sys
import time
import webbrowser
import shutil
import urllib.parse

# ------------- CONFIG -------------
AUTO_OPEN = True        # لینک‌ها خودکار باز می‌شن اگر دامنه در WHITELIST باشه
WHITELIST = ["t.me"]    # دامنه‌های مورد اعتماد
FAST_MODE = True
# ----------------------------------

# رنگ‌ها و استایل
GREEN = "\033[32m"
BRIGHT_GREEN = "\033[92m"
YELLOW = "\033[33m"
BRIGHT_YELLOW = "\033[93m"
RED = "\033[31m"
BRIGHT_RED = "\033[91m"
BG_RED = "\033[41m"
FG_WHITE = "\033[97m"
BOLD = "\033[1m"
UNDER = "\033[4m"
RESET = "\033[0m"

# آیتم‌ها (نام، لینک)
items = [
    ("Virus", "https://t.me/Xfxgtx_bot?start=B_6d4351"),
    ("Supervirus", "https://t.me/Xfxgtx_bot?start=B_ceba7c"),
    ("Veryyyyyy super virus", "https://t.me/Xfxgtx_bot?start=B_53cfc2"),
    ("MegaVirus", "https://t.me/Xfxgtx_bot?start=B_abcdef"),
    ("Vip verus5", "https://t.me/Xfxgtx_bot?start=B_c8d0ef"),
    ("Phishingvip", "https://t.me/Xfxgtx_bot?start=B_75f9df"),
    ("Camera hack", "https://t.me/Xfxgtx_bot?start=B_13e725"),
    ("Phishing", "https://t.me/Xfxgtx_bot?start=B_eb078b"),
    ("Massege hack", "https://t.me/Xfxgtx_bot?start=B_e8a450"),
    ("Singed apl", "https://t.me/Xfxgtx_bot?start=B_89bf70"),
]

# مالک‌ها 

= [
"████████████████████████████████████████████████████████████████",
"██                                                            ██",
"██          مالکان VIRUS TM                                   ██",
"██                                                            ██",
"██   OWNER 1: @Cybery_Person.    OWNER 2: @raef_skate.         ██",
"██                                                            ██",
"████████████████████████████████████████████████████████████████",
]

OWNER_LINE = BOLD + BRIGHT_RED + "مالک‌های virus tm: @Cybery_Person.   @raef_skate." + RESET

# ---------- utility ----------
def clear():
    os.system("clear")

def term_width():
    try:
        return shutil.get_terminal_size().columns
    except Exception:
        return 80

def center(text):
    w = term_width()
    return "\n".join(line.center(w) for line in str(text).splitlines())

def echo(text):
    if FAST_MODE:
        sys.stdout.write(text + "\n"); sys.stdout.flush()
    else:
        for ch in text:
            sys.stdout.write(ch); sys.stdout.flush(); time.sleep(0.001)
        sys.stdout.write("\n"); sys.stdout.flush()

def progress_bar(label="Opening", duration=0.6):
    width = min(36, max(20, term_width() // 3))
    for i in range(width + 1):
        pct = int(i / width * 100)
        bar = "[" + "#" * i + "-" * (width - i) + f"] {pct:3d}%"
        sys.stdout.write(center(BOLD + BRIGHT_YELLOW + f"{label} {bar}" + RESET) + "\r")
        sys.stdout.flush()
        time.sleep(duration / width)
    sys.stdout.write("\n"); sys.stdout.flush()

def domain_of(url):
    try:
        host = urllib.parse.urlparse(url).hostname or ""
        return host.lower().lstrip("www.")
    except Exception:
        return ""

# ---------- UI parts ----------
def print_owner_banner():
    # نمایش بنر مالک‌ها در بالای صفحه (بسیار بزرگ)
    for line in OWNER_BIG:
        echo(center(BOLD + BRIGHT_RED + line + RESET))

def print_logo():
    logo = [
        "██╗   ██╗██╗██████╗ ██╗   ██╗███████╗",
        "██║   ██║██║██╔══██╗██║   ██║██╔════╝",
        "██║   ██║██║██████╔╝██║   ██║█████╗  ",
        "╚██╗ ██╔╝██║██╔═══╝ ██║   ██║██╔══╝  ",
        " ╚████╔╝ ██║██║     ╚██████╔╝███████╗",
        "  ╚═══╝  ╚═╝╚═╝      ╚═════╝ ╚══════╝",
    ]
    colors = [BRIGHT_GREEN, GREEN, BRIGHT_YELLOW, YELLOW, BRIGHT_RED, RED]
    for i, l in enumerate(logo):
        echo(center(BOLD + colors[i % len(colors)] + l + RESET))

def render_box(idx, name):
    w = min(78, term_width() - 6)
    inner = w - 18
    label = name[:inner]
    pad_total = inner - len(label)
    pad_left = pad_total // 2
    pad_right = pad_total - pad_left

    top = BRIGHT_RED + BOLD + "╔" + "═" * (w - 2) + "╗" + RESET
    bottom = BRIGHT_RED + BOLD + "╚" + "═" * (w - 2) + "╝" + RESET
    num_box = BRIGHT_RED + BOLD + "[" + str(idx).rjust(3) + "]" + RESET

    # watermark مالک‌ها داخل کارت (خط کوچک زیر متن)
    watermark = BRIGHT_RED + BOLD + "  " + OWNER_LINE + RESET
    # اگر طول watermark بیش از inner باشد، کوتاهش کن
    watermark = watermark[: inner + 20]

    middle = (
        BRIGHT_RED + BOLD + "║ " + RESET
        + BG_RED + FG_WHITE + BOLD + " " * pad_left + label + " " * pad_right + RESET
        + "   " + num_box + BRIGHT_RED + BOLD + " ║" + RESET
    )
    # combine: top, middle, watermark line (centered inside box), bottom
    wm_line = BRIGHT_RED + BOLD + "║ " + RESET + watermark.center(w - 4) + BRIGHT_RED + BOLD + " ║" + RESET
    return top + "\n" + middle + "\n" + wm_line + "\n" + bottom

def render_menu(filtered=None):
    clear()
    print_owner_banner()         # بنر مالک‌ها بالای صفحه
    print_logo()
    echo("")
    echo(center(BOLD + BRIGHT_GREEN + "انتخاب فایل‌ها — عدد بزنید، s برای جستجو، q برای خروج" + RESET))
    echo("")
    data = filtered if filtered is not None else list(enumerate(items, start=1))
    for idx, (name, link) in data:
        box = render_box(idx, name)
        echo(center(box))
    echo("")
    echo(center(BOLD + BRIGHT_YELLOW + f"مجموع آیتم‌ها: {len(data)}" + RESET))

def search_menu():
    echo(center(BRIGHT_YELLOW + "جستجو: بخشی از نام را وارد کن و Enter بزن" + RESET))
    term = input(center(BOLD + BRIGHT_GREEN + "جستجو: " + RESET)).strip().lower()
    if not term:
        return None
    results = []
    for i, (name, link) in enumerate(items, start=1):
        if term in name.lower():
            results.append((i, (name, link)))
    if not results:
        echo(center(BRIGHT_RED + "هیچ موردی پیدا نشد." + RESET))
        time.sleep(0.5)
        return None
    return results

# ---------- auto-open logic ----------
def auto_open_if_allowed(idx):
    name, link = items[idx - 1]
    dom = domain_of(link)
    echo(center(BOLD + BRIGHT_YELLOW + f"آیتم انتخاب شده: {name}" + RESET))
    echo(center(BOLD + GREEN + f"لینک: {link}" + RESET))
    if AUTO_OPEN and (dom in WHITELIST):
        echo(center(BRIGHT_YELLOW + f"دامنه '{dom}' در WHITELIST یافت شد — باز شدن خودکار..." + RESET))
        progress_bar("Opening")
        try:
            webbrowser.open(link)
            echo(center(BOLD + BRIGHT_GREEN + f"[✔] لینک {name} باز شد." + RESET))
        except Exception as e:
            echo(center(BOLD + BRIGHT_RED + f"[✖] خطا هنگام باز کردن لینک: {e}" + RESET))
        return
    # not whitelisted => quick confirm
    echo(center(BRIGHT_YELLOW + f"دامنه '{dom}' در WHITELIST نیست. برای باز شدن سریع کلید 'o' را بزن (یا Enter برای لغو):" + RESET))
    ans = input(center(BOLD + BRIGHT_GREEN + "فشار کلید: " + RESET)).strip().lower()
    if ans == "o":
        progress_bar("Opening")
        try:
            webbrowser.open(link)
            echo(center(BOLD + BRIGHT_GREEN + f"[✔] لینک {name} باز شد." + RESET))
        except Exception as e:
            echo(center(BOLD + BRIGHT_RED + f"[✖] خطا هنگام باز کردن لینک: {e}" + RESET))
    else:
        echo(center(BRIGHT_RED + "باز نشد — تایید انجام نشد." + RESET))

def print_footer():
    echo("")
    # فوتر بسیار برجسته با مالک‌ها
    for line in OWNER_BIG:
        echo(center(BOLD + BRIGHT_RED + line + RESET))
    echo(center(BOLD + BRIGHT_RED + "مالک‌های virus tm: @Cybery_Person.   @raef_skate." + RESET))
    echo("")

# ---------- main loop ----------
def main():
    indexed = list(enumerate(items, start=1))
    while True:
        render_menu(indexed)
        choice = input(center(BOLD + BRIGHT_GREEN + "انتخاب شما (عدد / s / q): " + RESET)).strip()
        if not choice:
            continue
        if choice.lower() == "q":
            echo(center(BRIGHT_GREEN + "خروج. موفق باشی!" + RESET))
            print_footer()
            break
        if choice.lower() == "s":
            res = search_menu()
            if res:
                indexed = res
            else:
                indexed = list(enumerate(items, start=1))
            continue
        try:
            n = int(choice)
            if 1 <= n <= len(items):
                auto_open_if_allowed(n)
            else:
                echo(center(BRIGHT_RED + "❌ عدد خارج بازه." + RESET))
            indexed = list(enumerate(items, start=1))
            time.sleep(0.25)
        except ValueError:
            echo(center(BRIGHT_RED + "❌ ورودی نامعتبر — عدد یا s یا q وارد کن." + RESET))
            time.sleep(0.3)

if __name__ == "__main__":
    main()
