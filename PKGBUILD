pkgname=deltachat-desktop-git
pkgver=20181214
pkgrel=1
pkgdesc="A privacy oriented chat application built on e-mail"
arch=("any")
url="https://github.com/deltachat/deltachat-desktop"
license=("unknown")
depends=('openssl' 'sqlite' 'libsasl' 'zlib' 'bzip2' 'electron')
makedepends=("npm" "git")
source=(
    "deltachat-desktop-git::git://github.com/deltachat/deltachat-desktop.git#branch=master"
    "deltachat-desktop.desktop"
    "deltachat-desktop.sh"
)
sha256sums=(
    "SKIP"
    "SKIP"
    "SKIP"
)

prepare() {
    cd "$srcdir/${pkgname}"

    npm install
    npm run build
    
    # Delete development dependencies, we don't need them anymore
    npm prune --production    
}


package() {
    cd "$srcdir/${pkgname}"
    
    install -d "${pkgdir}/opt/DeltaChat/electron_app"
    cp -r ./node_modules "${pkgdir}/opt/DeltaChat/electron_app"
    cp -r ./src "${pkgdir}/opt/DeltaChat/electron_app"
    cp -r ./images "${pkgdir}/opt/DeltaChat/electron_app"
    cp -r ./build "${pkgdir}/opt/DeltaChat/electron_app"
    cp -r ./static "${pkgdir}/opt/DeltaChat/electron_app"
    cp -r ./_locales "${pkgdir}/opt/DeltaChat/electron_app"
    cp index.js "${pkgdir}/opt/DeltaChat/electron_app"
    cp package.json "${pkgdir}/opt/DeltaChat/electron_app"    
    
    install -d "${pkgdir}/opt/DeltaChat/electron_app/conversations"
    cp -r ./conversations/build "${pkgdir}/opt/DeltaChat/electron_app/conversations"
    
    install -Dm644 "${srcdir}/deltachat-desktop.desktop" "${pkgdir}/usr/share/applications/deltachat.desktop"
    install -Dm755 "${srcdir}/deltachat-desktop.sh" "${pkgdir}/opt/DeltaChat/deltachat"
    
    install -Dm644 ./images/deltachat.png "${pkgdir}/usr/share/icons/hicolor/scalable/apps/deltachat.png"
}
 
