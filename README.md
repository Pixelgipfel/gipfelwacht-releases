# GIPFELWACHT – offizielle Windows-Releases

Dieses Repository ist der öffentliche, **nur für Release-Artefakte bestimmte**
Downloadkanal von Pixelgipfel AG. Der private Produktquellcode und der
Lizenzdienst werden getrennt betrieben.

## Status

Aktuell gibt es **noch keinen freigegebenen Kundenrelease**. Vor dem ersten
Download müssen Code-Signing, Windows-11-Abnahme, Rechtstexte und der
Shop-/Lizenzierungsweg vollständig geprüft sein.

Offizielle Veröffentlichungen erscheinen ausschließlich unter
[Releases](https://github.com/Pixelgipfel/gipfelwacht-releases/releases).
Ein Kundenrelease enthält mindestens:

- `GIPFELWACHT-Setup-<VERSION>-x64.exe`;
- die zugehörige `.sha256`-Datei;
- `GIPFELWACHT-<TAG>-provenance.json` mit Quellcommit und Buildlauf;
- nachvollziehbare Release Notes.

Unsigned Dateien mit `TEST-UNSIGNED` im Namen sind interne Prüfbauten und
werden hier nicht veröffentlicht.

GitHub kann pro Release automatisch „Source code“-Archive dieses kleinen
Artefaktrepositories anzeigen. Diese Archive sind **weder** der
GIPFELWACHT-Quellcode **noch** der Windows-Installer.

## Download verifizieren

Nach einer offiziellen Veröffentlichung in PowerShell:

```powershell
Get-FileHash .\GIPFELWACHT-Setup-<VERSION>-x64.exe -Algorithm SHA256
Get-AuthenticodeSignature .\GIPFELWACHT-Setup-<VERSION>-x64.exe |
  Format-List Status,SignerCertificate,TimeStamperCertificate
```

Der Hash muss exakt zur veröffentlichten `.sha256`-Datei passen. Die
Authenticode-Prüfung muss `Valid` melden und als Herausgeber die in den
Release Notes genannte Pixelgipfel-Organisation anzeigen. Bei einer
Abweichung die Datei nicht starten.

Für dieses Repository sind unveränderliche GitHub-Releases aktiviert. Mit
einer aktuellen GitHub CLI lässt sich zusätzlich prüfen, ob die lokale Datei
exakt zum veröffentlichten Release-Artefakt gehört:

```powershell
gh release verify-asset <TAG> .\GIPFELWACHT-Setup-<VERSION>-x64.exe `
  --repo Pixelgipfel/gipfelwacht-releases
```

## Support und Sicherheitsmeldungen

- Support: [info@pixelgipfel.ch](mailto:info@pixelgipfel.ch)
- Sicherheitsprobleme bitte **nicht öffentlich** als Issue veröffentlichen;
  stattdessen die Hinweise in [SECURITY.md](SECURITY.md) verwenden.

## Rechte

Die Nutzung eines Release-Artefakts richtet sich nach den jeweils
mitgelieferten Produktbedingungen und Drittanbieterhinweisen. Dieses
Artefakt-Repository erteilt für sich allein keine zusätzlichen Rechte und
ändert keine Rechte aus eingebundenen Open-Source-Lizenzen.
