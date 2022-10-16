# sample_flutter_app

```mermaid
classDiagram
class DefaultFirebaseOptions
DefaultFirebaseOptions : +android$ FirebaseOptions
DefaultFirebaseOptions o-- FirebaseOptions
DefaultFirebaseOptions : +ios$ FirebaseOptions
DefaultFirebaseOptions o-- FirebaseOptions
DefaultFirebaseOptions : +currentPlatform$ FirebaseOptions
DefaultFirebaseOptions o-- FirebaseOptions

class MyApp
MyApp : -_router$ GoRouter
MyApp o-- GoRouter
MyApp : +playerProgressPersistence PlayerProgressPersistence
MyApp o-- PlayerProgressPersistence
MyApp : +settingsPersistence SettingsPersistence
MyApp o-- SettingsPersistence
MyApp : +gamesServicesController GamesServicesController?
MyApp o-- GamesServicesController
MyApp : +inAppPurchaseController InAppPurchaseController?
MyApp o-- InAppPurchaseController
MyApp : +adsController AdsController?
MyApp o-- AdsController
MyApp : +build() Widget
StatelessWidget <|-- MyApp

class AdsController
AdsController : -_instance MobileAds
AdsController o-- MobileAds
AdsController : -_preloadedAd PreloadedBannerAd?
AdsController o-- PreloadedBannerAd
AdsController : +dispose() void
AdsController : +initialize() void
AdsController : +preloadAd() void
AdsController : +takePreloadedAd() PreloadedBannerAd?

class BannerAdWidget
BannerAdWidget : +createState() State<BannerAdWidget>
StatefulWidget <|-- BannerAdWidget

class _BannerAdWidgetState
_BannerAdWidgetState : -_log$ Logger
_BannerAdWidgetState o-- Logger
_BannerAdWidgetState : -_bannerAd BannerAd?
_BannerAdWidgetState o-- BannerAd
_BannerAdWidgetState : -_adLoadingState _LoadingState
_BannerAdWidgetState o-- _LoadingState
_BannerAdWidgetState : -_currentOrientation Orientation
_BannerAdWidgetState o-- Orientation
_BannerAdWidgetState : +useAnchoredAdaptiveSize$ bool
_BannerAdWidgetState : +build() Widget
_BannerAdWidgetState : +initState() void
_BannerAdWidgetState : -_showPreloadedAd() void
_BannerAdWidgetState : +didChangeDependencies() void
_BannerAdWidgetState : +dispose() void
_BannerAdWidgetState : -_loadAd() Future<void>
State <|-- _BannerAdWidgetState

class _LoadingState
<<enumeration>> _LoadingState
_LoadingState : +index int
_LoadingState : +values$ List~_LoadingState~
_LoadingState : +initial$ _LoadingState
_LoadingState o-- _LoadingState
_LoadingState : +loading$ _LoadingState
_LoadingState o-- _LoadingState
_LoadingState : +disposing$ _LoadingState
_LoadingState o-- _LoadingState
_LoadingState : +loaded$ _LoadingState
_LoadingState o-- _LoadingState
Enum <|.. _LoadingState

class PreloadedBannerAd
PreloadedBannerAd : -_log$ Logger
PreloadedBannerAd o-- Logger
PreloadedBannerAd : +size AdSize
PreloadedBannerAd o-- AdSize
PreloadedBannerAd : -_adRequest AdRequest
PreloadedBannerAd o-- AdRequest
PreloadedBannerAd : -_bannerAd BannerAd?
PreloadedBannerAd o-- BannerAd
PreloadedBannerAd : +adUnitId String
PreloadedBannerAd : -_adCompleter Completer~BannerAd~
PreloadedBannerAd o-- Completer~BannerAd~
PreloadedBannerAd : +ready Future~BannerAd~
PreloadedBannerAd : +load() Future<void>
PreloadedBannerAd : +dispose() void

class SettingsScreen
SettingsScreen : -_gap$ SizedBox
SettingsScreen o-- SizedBox
SettingsScreen : +build() Widget
StatelessWidget <|-- SettingsScreen

class _NameChangeLine
_NameChangeLine : +title String
_NameChangeLine : +build() Widget
StatelessWidget <|-- _NameChangeLine

class _SettingsLine
_SettingsLine : +title String
_SettingsLine : +icon Widget
_SettingsLine o-- Widget
_SettingsLine : +onSelected void Function?
_SettingsLine o-- void Function
_SettingsLine : +build() Widget
StatelessWidget <|-- _SettingsLine

class CustomNameDialog
CustomNameDialog : +animation Animation~double~
CustomNameDialog o-- Animation~double~
CustomNameDialog : +createState() State<CustomNameDialog>
StatefulWidget <|-- CustomNameDialog

class _CustomNameDialogState
_CustomNameDialogState : -_controller TextEditingController
_CustomNameDialogState o-- TextEditingController
_CustomNameDialogState : +build() Widget
_CustomNameDialogState : +didChangeDependencies() void
_CustomNameDialogState : +dispose() void
State <|-- _CustomNameDialogState

class MemoryOnlySettingsPersistence
MemoryOnlySettingsPersistence : +musicOn bool
MemoryOnlySettingsPersistence : +soundsOn bool
MemoryOnlySettingsPersistence : +muted bool
MemoryOnlySettingsPersistence : +playerName String
MemoryOnlySettingsPersistence : +getMusicOn() Future<bool>
MemoryOnlySettingsPersistence : +getMuted() Future<bool>
MemoryOnlySettingsPersistence : +getPlayerName() Future<String>
MemoryOnlySettingsPersistence : +getSoundsOn() Future<bool>
MemoryOnlySettingsPersistence : +saveMusicOn() Future<void>
MemoryOnlySettingsPersistence : +saveMuted() Future<void>
MemoryOnlySettingsPersistence : +savePlayerName() Future<void>
MemoryOnlySettingsPersistence : +saveSoundsOn() Future<void>
SettingsPersistence <|.. MemoryOnlySettingsPersistence

class SettingsPersistence
<<abstract>> SettingsPersistence
SettingsPersistence : +getMusicOn()* Future<bool>
SettingsPersistence : +getMuted()* Future<bool>
SettingsPersistence : +getPlayerName()* Future<String>
SettingsPersistence : +getSoundsOn()* Future<bool>
SettingsPersistence : +saveMusicOn()* Future<void>
SettingsPersistence : +saveMuted()* Future<void>
SettingsPersistence : +savePlayerName()* Future<void>
SettingsPersistence : +saveSoundsOn()* Future<void>

class LocalStorageSettingsPersistence
LocalStorageSettingsPersistence : +instanceFuture Future~SharedPreferences~
LocalStorageSettingsPersistence : +getMusicOn() Future<bool>
LocalStorageSettingsPersistence : +getMuted() Future<bool>
LocalStorageSettingsPersistence : +getPlayerName() Future<String>
LocalStorageSettingsPersistence : +getSoundsOn() Future<bool>
LocalStorageSettingsPersistence : +saveMusicOn() Future<void>
LocalStorageSettingsPersistence : +saveMuted() Future<void>
LocalStorageSettingsPersistence : +savePlayerName() Future<void>
LocalStorageSettingsPersistence : +saveSoundsOn() Future<void>
SettingsPersistence <|-- LocalStorageSettingsPersistence

class SettingsController
SettingsController : -_persistence SettingsPersistence
SettingsController o-- SettingsPersistence
SettingsController : +muted ValueNotifier~bool~
SettingsController o-- ValueNotifier~bool~
SettingsController : +playerName ValueNotifier~String~
SettingsController o-- ValueNotifier~String~
SettingsController : +soundsOn ValueNotifier~bool~
SettingsController o-- ValueNotifier~bool~
SettingsController : +musicOn ValueNotifier~bool~
SettingsController o-- ValueNotifier~bool~
SettingsController : +loadStateFromPersistence() Future<void>
SettingsController : +setPlayerName() void
SettingsController : +toggleMusicOn() void
SettingsController : +toggleMuted() void
SettingsController : +toggleSoundsOn() void

class MainMenuScreen
MainMenuScreen : +build() Widget
MainMenuScreen : -_hideUntilReady() Widget
StatelessWidget <|-- MainMenuScreen

class GamesServicesController
GamesServicesController : -_log$ Logger
GamesServicesController o-- Logger
GamesServicesController : -_signedInCompleter Completer~bool~
GamesServicesController o-- Completer~bool~
GamesServicesController : +signedIn Future~bool~
GamesServicesController : +initialize() void
GamesServicesController : +showAchievements() void
GamesServicesController : +showLeaderboard() void
GamesServicesController : +awardAchievement() void
GamesServicesController : +submitLeaderboardScore() void

class Score
Score : +score int
Score : +duration Duration
Score : +level int
Score : +formattedTime String
Score : +toString() String

class Tile
Tile : +x int
Tile : +y int
Tile : +hashCode int
Tile : +==() bool
Tile : +isValid() bool
Tile : +toPointer() int
Tile : +toString() String

class BoardState
BoardState : -_log$ Logger
BoardState o-- Logger
BoardState : +setting BoardSetting
BoardState o-- BoardSetting
BoardState : +aiOpponent AiOpponent
BoardState o-- AiOpponent
BoardState : -_xTaken Set~int~
BoardState : -_oTaken Set~int~
BoardState : -_latestXTile Tile?
BoardState o-- Tile
BoardState : -_latestOTile Tile?
BoardState o-- Tile
BoardState : -_isLocked bool
BoardState : +playerWon ChangeNotifier
BoardState o-- ChangeNotifier
BoardState : +aiOpponentWon ChangeNotifier
BoardState o-- ChangeNotifier
BoardState : -_winningLine List~Tile~?
BoardState : +isLocked bool
BoardState : +winningLine Iterable~Tile~?
BoardState : -_allTakenTiles Iterable~Tile~
BoardState : -_allTiles Iterable~Tile~
BoardState : -_hasOpenTiles bool
BoardState : +canTake() bool
BoardState : +clearBoard() void
BoardState : +initialize() void
BoardState : +dispose() void
BoardState : +getLatestTileForSide() Tile?
BoardState : +getNeighborhood() Iterable<Tile>
BoardState : +getValidLinesThrough() Iterable<List<Tile>>
BoardState : +take() void
BoardState : +whoIsAt() Side
BoardState : -_getWinner() Side?
BoardState : -_selectSet() Set<int>
BoardState : -_takeTile() void
BoardState : -_generateInitialOTaken() Set<int>
ChangeNotifier <|-- BoardState

class Side
<<enumeration>> Side
Side : +index int
Side : +values$ List~Side~
Side : +x$ Side
Side o-- Side
Side : +o$ Side
Side o-- Side
Side : +none$ Side
Side o-- Side
Enum <|.. Side

class BoardSetting
BoardSetting : +m int
BoardSetting : +n int
BoardSetting : +k int
BoardSetting : +playerSide Side
BoardSetting o-- Side
BoardSetting : +aiStarts bool
BoardSetting : +aiOpponentSide Side
BoardSetting o-- Side
BoardSetting : +hashCode int
BoardSetting : +==() bool

class InAppPurchaseController
InAppPurchaseController : -_log$ Logger
InAppPurchaseController o-- Logger
InAppPurchaseController : -_subscription StreamSubscriptionListPurchaseDetails~~?
InAppPurchaseController o-- StreamSubscriptionListPurchaseDetails~~
InAppPurchaseController : +inAppPurchaseInstance InAppPurchase
InAppPurchaseController o-- InAppPurchase
InAppPurchaseController : -_adRemoval AdRemovalPurchase
InAppPurchaseController o-- AdRemovalPurchase
InAppPurchaseController : +adRemoval AdRemovalPurchase
InAppPurchaseController o-- AdRemovalPurchase
InAppPurchaseController : +buy() Future<void>
InAppPurchaseController : +dispose() void
InAppPurchaseController : +restorePurchases() Future<void>
InAppPurchaseController : +subscribe() void
InAppPurchaseController : -_listenToPurchaseUpdated() Future<void>
InAppPurchaseController : -_reportError() void
InAppPurchaseController : -_verifyPurchase() Future<bool>
ChangeNotifier <|-- InAppPurchaseController

class AdRemovalPurchase
AdRemovalPurchase : +productId$ String
AdRemovalPurchase : +active bool
AdRemovalPurchase : +pending bool
AdRemovalPurchase : +error Object?
AdRemovalPurchase : +hashCode int
AdRemovalPurchase : +==() bool

class AnimatedSprite
AnimatedSprite : +image ImageProvider~Object~
AnimatedSprite o-- ImageProvider~Object~
AnimatedSprite : +frameWidth int
AnimatedSprite : +frameHeight int
AnimatedSprite : +frameStart int
AnimatedSprite : +frameCount int
AnimatedSprite : +color Color?
AnimatedSprite o-- Color
AnimatedSprite : +flipHorizontally bool
AnimatedSprite : +build() Widget
AnimatedWidget <|-- AnimatedSprite

class Sprite
Sprite : +image ImageProvider~Object~
Sprite o-- ImageProvider~Object~
Sprite : +frameWidth int
Sprite : +frameHeight int
Sprite : +frame int
Sprite : +color Color?
Sprite o-- Color
Sprite : +flipHorizontally bool
Sprite : +createState() State<Sprite>
StatefulWidget <|-- Sprite

class _SpritePainter
_SpritePainter : +image Image
_SpritePainter o-- Image
_SpritePainter : +rect Rect
_SpritePainter o-- Rect
_SpritePainter : +color Color?
_SpritePainter o-- Color
_SpritePainter : +flipHorizontally bool
_SpritePainter : -_paint Paint
_SpritePainter o-- Paint
_SpritePainter : +paint() void
_SpritePainter : +shouldRepaint() bool
CustomPainter <|-- _SpritePainter

class _SpriteState
_SpriteState : -_imageStream ImageStream?
_SpriteState o-- ImageStream
_SpriteState : -_imageInfo ImageInfo?
_SpriteState o-- ImageInfo
_SpriteState : +build() Widget
_SpriteState : +didChangeDependencies() void
_SpriteState : +didUpdateWidget() void
_SpriteState : +dispose() void
_SpriteState : +initState() void
_SpriteState : -_getImage() void
_SpriteState : -_updateImage() void
State <|-- _SpriteState

class Palette
Palette : +pen Color
Palette o-- Color
Palette : +darkPen Color
Palette o-- Color
Palette : +redPen Color
Palette o-- Color
Palette : +inkFullOpacity Color
Palette o-- Color
Palette : +ink Color
Palette o-- Color
Palette : +backgroundMain Color
Palette o-- Color
Palette : +backgroundLevelSelection Color
Palette o-- Color
Palette : +backgroundPlaySession Color
Palette o-- Color
Palette : +background4 Color
Palette o-- Color
Palette : +backgroundSettings Color
Palette o-- Color
Palette : +trueWhite Color
Palette o-- Color

class RoughButton
RoughButton : +child Widget
RoughButton o-- Widget
RoughButton : +onTap void Function?
RoughButton o-- void Function
RoughButton : +textColor Color?
RoughButton o-- Color
RoughButton : +drawRectangle bool
RoughButton : +fontSize double
RoughButton : +soundEffect SfxType
RoughButton o-- SfxType
RoughButton : -_handleTap() void
RoughButton : +build() Widget
StatelessWidget <|-- RoughButton

class _RoughBox
_RoughBox : +image ImageProvider~Object~
_RoughBox o-- ImageProvider~Object~
_RoughBox : +createState() State<_RoughBox>
StatefulWidget <|-- _RoughBox

class _RoughBoxState
_RoughBoxState : -_imageStream ImageStream?
_RoughBoxState o-- ImageStream
_RoughBoxState : -_imageInfo ImageInfo?
_RoughBoxState o-- ImageInfo
_RoughBoxState : +build() Widget
_RoughBoxState : +didChangeDependencies() void
_RoughBoxState : +didUpdateWidget() void
_RoughBoxState : +dispose() void
_RoughBoxState : +initState() void
_RoughBoxState : -_getImage() void
_RoughBoxState : -_updateImage() void
State <|-- _RoughBoxState

class _RoughBoxPainter
_RoughBoxPainter : +image Image
_RoughBoxPainter o-- Image
_RoughBoxPainter : +paint() void
_RoughBoxPainter : +shouldRepaint() bool
CustomPainter <|-- _RoughBoxPainter

class DelayedAppear
DelayedAppear : +child Widget
DelayedAppear o-- Widget
DelayedAppear : +delay Duration
DelayedAppear : +delayStateCreation bool
DelayedAppear : +onDelayFinished void Function?
DelayedAppear o-- void Function
DelayedAppear : +createState() State<DelayedAppear>
StatefulWidget <|-- DelayedAppear

class _DelayedAppearState
_DelayedAppearState : +fadeDuration$ Duration
_DelayedAppearState : -_delayController AnimationController
_DelayedAppearState o-- AnimationController
_DelayedAppearState : -_fadeController AnimationController
_DelayedAppearState o-- AnimationController
_DelayedAppearState : -_delayFinished bool
_DelayedAppearState : +build() Widget
_DelayedAppearState : +initState() void
_DelayedAppearState : +dispose() void
State <|-- _DelayedAppearState
TickerProviderStateMixin <|-- _DelayedAppearState

class ScreenDelays
ScreenDelays : -_cadence$ int
ScreenDelays : +first$ int
ScreenDelays : +second$ int
ScreenDelays : +third$ int
ScreenDelays : +fourth$ int
ScreenDelays : +fifth$ int

class _InkReveal
_InkReveal : +child Widget
_InkReveal o-- Widget
_InkReveal : +animation Animation~double~
_InkReveal o-- Animation~double~
_InkReveal : +color Color
_InkReveal o-- Color
_InkReveal : +flipHorizontally bool
_InkReveal : +createState() State<_InkReveal>
StatefulWidget <|-- _InkReveal

class _InkRevealState
_InkRevealState : -_log$ Logger
_InkRevealState o-- Logger
_InkRevealState : -_finished bool
_InkRevealState : +initState() void
_InkRevealState : +didUpdateWidget() void
_InkRevealState : +dispose() void
_InkRevealState : +build() Widget
_InkRevealState : -_statusListener() void
State <|-- _InkRevealState

class Confetti
Confetti : -_defaultColors$ List~Color~
Confetti : +isStopped bool
Confetti : +colors List~Color~
Confetti : +createState() State<Confetti>
StatefulWidget <|-- Confetti

class ConfettiPainter
ConfettiPainter : +defaultPaint Paint
ConfettiPainter o-- Paint
ConfettiPainter : +snippingsCount int
ConfettiPainter : -_snippings List~_PaperSnipping~
ConfettiPainter : -_size Size?
ConfettiPainter o-- Size
ConfettiPainter : -_lastTime DateTime
ConfettiPainter : +colors UnmodifiableListView~Color~
ConfettiPainter o-- UnmodifiableListView~Color~
ConfettiPainter : +paint() void
ConfettiPainter : +shouldRepaint() bool
CustomPainter <|-- ConfettiPainter

class _ConfettiState
_ConfettiState : -_controller AnimationController
_ConfettiState o-- AnimationController
_ConfettiState : +build() Widget
_ConfettiState : +didUpdateWidget() void
_ConfettiState : +dispose() void
_ConfettiState : +initState() void
State <|-- _ConfettiState
SingleTickerProviderStateMixin <|-- _ConfettiState

class _PaperSnipping
_PaperSnipping : -_random$ Random
_PaperSnipping o-- Random
_PaperSnipping : +degToRad$ double
_PaperSnipping : +backSideBlend$ Color
_PaperSnipping o-- Color
_PaperSnipping : -_bounds Size
_PaperSnipping o-- Size
_PaperSnipping : +position _Vector
_PaperSnipping o-- _Vector
_PaperSnipping : +rotationSpeed double
_PaperSnipping : +angle double
_PaperSnipping : +rotation double
_PaperSnipping : +cosA double
_PaperSnipping : +size double
_PaperSnipping : +oscillationSpeed double
_PaperSnipping : +xSpeed double
_PaperSnipping : +ySpeed double
_PaperSnipping : +corners List~_Vector~
_PaperSnipping : +time double
_PaperSnipping : +frontColor Color
_PaperSnipping o-- Color
_PaperSnipping : +backColor Color
_PaperSnipping o-- Color
_PaperSnipping : +paint Paint
_PaperSnipping o-- Paint
_PaperSnipping : +draw() void
_PaperSnipping : +update() void
_PaperSnipping : +updateBounds() void

class _Vector
_Vector : +x double
_Vector : +y double

class ResponsiveScreen
ResponsiveScreen : +squarishMainArea Widget
ResponsiveScreen o-- Widget
ResponsiveScreen : +rectangularMenuArea Widget
ResponsiveScreen o-- Widget
ResponsiveScreen : +topMessageArea Widget
ResponsiveScreen o-- Widget
ResponsiveScreen : +mainAreaProminence double
ResponsiveScreen : +build() Widget
StatelessWidget <|-- ResponsiveScreen

class RoughGrid
RoughGrid : +width int
RoughGrid : +height int
RoughGrid : +build() Widget
StatelessWidget <|-- RoughGrid

class _RoughGridPainter
_RoughGridPainter : +width int
_RoughGridPainter : +height int
_RoughGridPainter : +lineColor Color
_RoughGridPainter o-- Color
_RoughGridPainter : +paintOnly Axis?
_RoughGridPainter o-- Axis
_RoughGridPainter : +pathPaint Paint
_RoughGridPainter o-- Paint
_RoughGridPainter : -_random Random
_RoughGridPainter o-- Random
_RoughGridPainter : +paint() void
_RoughGridPainter : +shouldRepaint() bool
_RoughGridPainter : -_roughLine()$ void
CustomPainter <|-- _RoughGridPainter

class Board
Board : +onPlayerWon void Function?
Board o-- void Function
Board : +setting BoardSetting
Board o-- BoardSetting
Board : +createState() State<Board>
StatefulWidget <|-- Board

class _BoardState
_BoardState : +build() Widget
State <|-- _BoardState

class PlaySessionScreen
PlaySessionScreen : +level GameLevel
PlaySessionScreen o-- GameLevel
PlaySessionScreen : +createState() State<PlaySessionScreen>
StatefulWidget <|-- PlaySessionScreen

class _PlaySessionScreenState
_PlaySessionScreenState : -_log$ Logger
_PlaySessionScreenState o-- Logger
_PlaySessionScreenState : -_celebrationDuration$ Duration
_PlaySessionScreenState : -_preCelebrationDuration$ Duration
_PlaySessionScreenState : -_resetHint StreamController~void~
_PlaySessionScreenState o-- StreamController~void~
_PlaySessionScreenState : -_duringCelebration bool
_PlaySessionScreenState : -_startOfPlay DateTime
_PlaySessionScreenState : +opponent AiOpponent
_PlaySessionScreenState o-- AiOpponent
_PlaySessionScreenState : +build() Widget
_PlaySessionScreenState : +initState() void
_PlaySessionScreenState : -_aiOpponentWon() void
_PlaySessionScreenState : -_playerWon() void
State <|-- _PlaySessionScreenState

class _RestartButton
_RestartButton : +resetHint Stream~void~
_RestartButton o-- Stream~void~
_RestartButton : +onTap void Function
_RestartButton o-- void Function
_RestartButton : +createState() State<_RestartButton>
StatefulWidget <|-- _RestartButton

class _RestartButtonState
_RestartButtonState : -_controller AnimationController
_RestartButtonState o-- AnimationController
_RestartButtonState : -_subscription StreamSubscription~dynamic~?
_RestartButtonState o-- StreamSubscription~dynamic~
_RestartButtonState : -_bump$ TweenSequence~double~
_RestartButtonState o-- TweenSequence~double~
_RestartButtonState : +initState() void
_RestartButtonState : +didUpdateWidget() void
_RestartButtonState : +dispose() void
_RestartButtonState : +build() Widget
_RestartButtonState : -_handleResetHint() void
State <|-- _RestartButtonState
SingleTickerProviderStateMixin <|-- _RestartButtonState

class _ResponsivePlaySessionScreen
_ResponsivePlaySessionScreen : +mainBoardArea Widget
_ResponsivePlaySessionScreen o-- Widget
_ResponsivePlaySessionScreen : +backButtonArea Widget
_ResponsivePlaySessionScreen o-- Widget
_ResponsivePlaySessionScreen : +settingsButtonArea Widget
_ResponsivePlaySessionScreen o-- Widget
_ResponsivePlaySessionScreen : +restartButtonArea Widget
_ResponsivePlaySessionScreen o-- Widget
_ResponsivePlaySessionScreen : +playerName TextSpan
_ResponsivePlaySessionScreen o-- TextSpan
_ResponsivePlaySessionScreen : +opponentName TextSpan
_ResponsivePlaySessionScreen o-- TextSpan
_ResponsivePlaySessionScreen : +mainAreaProminence double
_ResponsivePlaySessionScreen : -_buildVersusText() Widget
_ResponsivePlaySessionScreen : +build() Widget
StatelessWidget <|-- _ResponsivePlaySessionScreen

class BoardTile
BoardTile : +tile Tile
BoardTile o-- Tile
BoardTile : -_log$ Logger
BoardTile o-- Logger
BoardTile : +createState() State<BoardTile>
StatefulWidget <|-- BoardTile

class _BoardTileState
_BoardTileState : -_controller AnimationController
_BoardTileState o-- AnimationController
_BoardTileState : -_previousOwner Side?
_BoardTileState o-- Side
_BoardTileState : +initState() void
_BoardTileState : +didChangeDependencies() void
_BoardTileState : +dispose() void
_BoardTileState : +build() Widget
State <|-- _BoardTileState
SingleTickerProviderStateMixin <|-- _BoardTileState

class _SketchedX
_SketchedX : +progress Animation~double~
_SketchedX o-- Animation~double~
_SketchedX : +color Color
_SketchedX o-- Color
_SketchedX : +variantSeed int
_SketchedX : -_startImageAssets$ List~String~
_SketchedX : -_endImageAssets$ List~String~
_SketchedX : +build() Widget
StatelessWidget <|-- _SketchedX

class _SketchedO
_SketchedO : +progress Animation~double~
_SketchedO o-- Animation~double~
_SketchedO : +color Color
_SketchedO o-- Color
_SketchedO : +variantSeed int
_SketchedO : -_imageAssets$ List~String~
_SketchedO : +build() Widget
StatelessWidget <|-- _SketchedO

class SfxType
<<enumeration>> SfxType
SfxType : +index int
SfxType : +values$ List~SfxType~
SfxType : +drawX$ SfxType
SfxType o-- SfxType
SfxType : +drawO$ SfxType
SfxType o-- SfxType
SfxType : +buttonTap$ SfxType
SfxType o-- SfxType
SfxType : +congrats$ SfxType
SfxType o-- SfxType
SfxType : +erase$ SfxType
SfxType o-- SfxType
SfxType : +drawGrid$ SfxType
SfxType o-- SfxType
Enum <|.. SfxType

class AudioController
AudioController : -_log$ Logger
AudioController o-- Logger
AudioController : -_musicCache AudioCache
AudioController o-- AudioCache
AudioController : -_sfxCache AudioCache
AudioController o-- AudioCache
AudioController : -_musicPlayer AudioPlayer
AudioController o-- AudioPlayer
AudioController : -_sfxPlayers List~AudioPlayer~
AudioController : -_currentSfxPlayer int
AudioController : -_playlist Queue~Song~
AudioController o-- Queue~Song~
AudioController : -_random Random
AudioController o-- Random
AudioController : -_settings SettingsController?
AudioController o-- SettingsController
AudioController : -_lifecycleNotifier ValueNotifier~AppLifecycleState~?
AudioController o-- ValueNotifier~AppLifecycleState~
AudioController : +attachLifecycleNotifier() void
AudioController : +attachSettings() void
AudioController : +dispose() void
AudioController : +initialize() void
AudioController : +playSfx() void
AudioController : -_changeSong() void
AudioController : -_handleAppLifecycle() void
AudioController : -_musicOnHandler() void
AudioController : -_mutedHandler() void
AudioController : -_resumeMusic() void
AudioController : -_soundsOnHandler() void
AudioController : -_startMusic() void
AudioController : -_stopAllSound() void
AudioController : -_stopMusic() void

class Song
Song : +filename String
Song : +author String
Song : +name String
Song : +toString() String

class RandomOpponent
RandomOpponent : -_random$ Random
RandomOpponent o-- Random
RandomOpponent : +name String
RandomOpponent : +chooseNextMove() Tile
AiOpponent <|-- RandomOpponent

class HumanlikeOpponent
HumanlikeOpponent : -_log$ Logger
HumanlikeOpponent o-- Logger
HumanlikeOpponent : +stubbornness double
HumanlikeOpponent : +bestPlayCount int
HumanlikeOpponent : +humanlikePlayCount int
HumanlikeOpponent : +name String
HumanlikeOpponent : +aiScoring List~int~
HumanlikeOpponent : +playerScoring List~int~
HumanlikeOpponent : +chooseNextMove() Tile
AiOpponent <|-- HumanlikeOpponent

class _TileScore
_TileScore : +tile Tile
_TileScore o-- Tile
_TileScore : +bestPlay int
_TileScore : +humanlikePlay int
_TileScore : +finalScore double?
_TileScore : +toString() String

class AiOpponent
<<abstract>> AiOpponent
AiOpponent : +setting BoardSetting
AiOpponent o-- BoardSetting
AiOpponent : +name String
AiOpponent : +chooseNextMove()* Tile

class ScoringOpponent
ScoringOpponent : +name String
ScoringOpponent : -_playerScoring List~int~
ScoringOpponent : -_aiScoring List~int~
ScoringOpponent : +chooseNextMove() Tile
AiOpponent <|-- ScoringOpponent

class AttackOnlyScoringOpponent
AttackOnlyScoringOpponent : -_playerScoring List~int~
AttackOnlyScoringOpponent : -_aiScoring List~int~
ScoringOpponent <|-- AttackOnlyScoringOpponent

class AppLifecycleObserver
AppLifecycleObserver : +child Widget
AppLifecycleObserver o-- Widget
AppLifecycleObserver : +createState() State<AppLifecycleObserver>
StatefulWidget <|-- AppLifecycleObserver

class _AppLifecycleObserverState
_AppLifecycleObserverState : -_log$ Logger
_AppLifecycleObserverState o-- Logger
_AppLifecycleObserverState : +lifecycleListenable ValueNotifier~AppLifecycleState~
_AppLifecycleObserverState o-- ValueNotifier~AppLifecycleState~
_AppLifecycleObserverState : +build() Widget
_AppLifecycleObserverState : +didChangeAppLifecycleState() void
_AppLifecycleObserverState : +dispose() void
_AppLifecycleObserverState : +initState() void
State <|-- _AppLifecycleObserverState
WidgetsBindingObserver <|-- _AppLifecycleObserverState

class LocalStoragePlayerProgressPersistence
LocalStoragePlayerProgressPersistence : +instanceFuture Future~SharedPreferences~
LocalStoragePlayerProgressPersistence : +getHighestLevelReached() Future<int>
LocalStoragePlayerProgressPersistence : +saveHighestLevelReached() Future<void>
PlayerProgressPersistence <|-- LocalStoragePlayerProgressPersistence

class MemoryOnlyPlayerProgressPersistence
MemoryOnlyPlayerProgressPersistence : +level int
MemoryOnlyPlayerProgressPersistence : +getHighestLevelReached() Future<int>
MemoryOnlyPlayerProgressPersistence : +saveHighestLevelReached() Future<void>
PlayerProgressPersistence <|.. MemoryOnlyPlayerProgressPersistence

class PlayerProgressPersistence
<<abstract>> PlayerProgressPersistence
PlayerProgressPersistence : +getHighestLevelReached()* Future<int>
PlayerProgressPersistence : +saveHighestLevelReached()* Future<void>

class PlayerProgress
PlayerProgress : -_store PlayerProgressPersistence
PlayerProgress o-- PlayerProgressPersistence
PlayerProgress : -_highestLevelReached int
PlayerProgress : +maxHighestScoresPerPlayer$ int
PlayerProgress : +highestLevelReached int
PlayerProgress : +getLatestFromStore() void
PlayerProgress : +reset() void
PlayerProgress : +setLevelReached() void
ChangeNotifier <|-- PlayerProgress

class GameLevel
GameLevel : +number int
GameLevel : +setting BoardSetting
GameLevel o-- BoardSetting
GameLevel : +difficulty int
GameLevel : +aiOpponentBuilder AiOpponent FunctionBoardSetting
GameLevel o-- AiOpponent FunctionBoardSetting
GameLevel : +achievementIdIOS String?
GameLevel : +achievementIdAndroid String?
GameLevel : +awardsAchievement bool

class LevelSelectionScreen
LevelSelectionScreen : +build() Widget
StatelessWidget <|-- LevelSelectionScreen

class _LevelButton
_LevelButton : +number int
_LevelButton : +build() Widget
StatelessWidget <|-- _LevelButton

class WinGameScreen
WinGameScreen : +score Score
WinGameScreen o-- Score
WinGameScreen : +build() Widget
StatelessWidget <|-- WinGameScreen

```
